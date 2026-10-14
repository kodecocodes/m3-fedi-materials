# Draft Development Plan: AI Usage Insights

## Feature summary

Add one `AI Usage Insights` row to the existing Tokens Dashboard summary list. Selecting the row opens one `UsageInsightsView` that shows up to three compact, team-level review prompts derived from fixed mock data by deterministic local rules.

## Goals

- Help team leads, engineering managers, and project leads review aggregate AI usage patterns alongside delivery context.
- Preserve the app’s established summary-to-detail navigation pattern.
- Present observed changes as cautious review prompts, not conclusions.
- Keep the feature local, small, and testable.

## Non-goals

- Individual developer names, rankings, or performance judgments in insight cards.
- Runtime LLM calls, networking, persistence, authentication, or backend services.
- A tab bar, navigation redesign, or per-insight detail screens.
- Recommendations to use more AI.
- Claims that AI usage caused delivery improvements.
- Pricing advice or premium-model, standard-model, or cheap-model classifications.
- Forecasting, benchmarking, alerts, anomaly detection, or automated interventions.

## User flow

1. A user opens `SummaryView`.
2. The existing narrative list includes one new `AI Usage Insights` row.
3. Selecting the row navigates through `DestinationGraph` to `UsageInsightsView`.
4. The screen displays zero to three cards in a stable order: AI activity, model mix, then delivery context.
5. If comparison data is unavailable, the screen explains that more data is needed.
6. If valid comparisons exist but no rule qualifies, the screen says there are no notable team-level patterns for the period.

Cards are informational only in version 1. Do not add card-specific destinations.

## UI plan

The summary row should use the existing summary-row visual treatment and navigation affordance. Its copy should be brief and neutral, such as: “Review aggregate team usage patterns alongside delivery context.”

`UsageInsightsView` should contain:

- Navigation title: `AI Usage Insights`.
- Helper text: “Team-level patterns to review alongside delivery context.”
- Up to three compact insight cards.
- A clear insufficient-data state.
- A clear no-noteworthy-patterns state.

Each card should contain a neutral title, concise comparison evidence, and one cautious review prompt. Do not use warning colors, grades, rankings, urgency language, or causal statements. Trend icons, if used, are supplementary and must not be the only way information is conveyed.

## Proposed Swift surface

- `UsageInsight`: display model containing a stable category-based identity, title, evidence, review prompt, and optional display-only trend direction.
- `UsageInsightCategory`: closed set with `activity`, `modelMix`, and `deliveryContext` values.
- `UsageInsightsViewModel`: receives local store dependencies, converts them to aggregate inputs, and exposes one of three states: insights, no noteworthy patterns, or insufficient data.
- `UsageInsightBuilder`: pure, deterministic rule layer that receives aggregate period data only. It must not accept developer records or identity fields.
- `UsageInsightBuilder.Configuration`: one local surface for thresholds and stable rule configuration.
- `UsageInsightsView`: renders the cards or an informational state.

`SummaryViewModel` adds one summary row. `DestinationGraph` adds one `usageInsights` destination. No other navigation type is needed.

## Proposed files

### Add

- `Models/UsageInsight.swift`
- `ViewModels/UsageInsightsViewModel.swift`
- `Views/UsageInsightsView.swift`
- `UsageInsightBuilderTests.swift` in the app’s test target; add a small test target first if one does not yet exist.

### Modify

- `Views/SummaryView.swift`
- `ViewModels/SummaryViewModel.swift`
- `Models/CostbyModel.swift` to add fixed, local prior-period token values needed for period comparison.
- Project configuration only if the project does not automatically discover added Swift files.

Do not use `DeveloperOutcomeStore` in the version 1 insight flow because it provides individual-level records and no comparable historical period.

## Data flow

```text
ModelCostStore ──────→ aggregate current/prior token totals and model shares
TicketToMergeStore ──→ aggregate team delivery periods
                              ↓
                    UsageInsightBuilder
                              ↓
                       [UsageInsight]
                              ↓
                     UsageInsightsView
```

`ModelCostStore` is the version 1 source of truth for token activity and model mix. Add a fixed `previousTokens` value for each model to represent the immediately preceding equal-length period.

`TicketToMergeStore` provides delivery context. Aggregate the available cohort values into one monthly team value before passing them to the builder. Because cohort-size data is unavailable, use an unweighted arithmetic mean and label the result as context for review only.

## Insight rules

Use the current reporting period and the immediately preceding equal-length period. Suppress a rule when required values are missing, negative, non-finite, below the minimum volume, or unable to form a valid comparison. Evaluate thresholds using unrounded values; round only for display.

| Rule configuration | Version 1 default |
| --- | --- |
| Minimum comparison volume | 1,000,000 tokens in both periods |
| AI activity threshold | Absolute relative change of at least 15% |
| Model-mix threshold | Absolute share shift of at least 10 percentage points |
| Delivery-context threshold | Absolute relative change of at least 5% |
| Model-shift tie-breaker | Alphabetical model name after equal absolute shifts |
| Maximum card count | Three |

### AI activity

Compare total current and prior team token activity. Show a card only when both periods meet the minimum volume and the absolute relative change is at least 15%.

Example: “Team token activity increased 18% compared with the prior period. Review this alongside current project and delivery context.”

### Model mix

Compare each model’s share of total team tokens between periods. Show only the model with the largest absolute share shift when it reaches 10 percentage points. Do not describe any model as premium, standard, cheap, better, or preferred.

### Delivery context

Compare the latest two complete aggregate monthly ticket-to-merge values. Show the card when the absolute relative change is at least 5%. The card must state that this is delivery context for review, not evidence of cause.

## Edge cases

- No data or only one comparison period.
- Zero, negative, or non-finite values.
- Token totals below the configured minimum volume.
- A model present in only one period; treat the missing value as zero only when aggregate totals remain valid.
- Zero total model usage in either comparison period.
- Multiple models crossing the mix threshold; show the largest shift and apply the stated tie-breaker.
- One store unavailable while another supports a valid card; show valid cards rather than failing the screen.
- All comparisons valid but below thresholds; show the no-noteworthy-patterns state.
- Partial current periods; do not compare them with completed prior periods.
- Long strings and larger accessibility text sizes.

## Accessibility requirements

- Support Dynamic Type without clipping card content or informational states.
- Maintain adequate contrast for text and card surfaces.
- Do not rely on color, direction icons, or chart position alone to convey a trend.
- Keep the summary row and any future navigation affordance large enough to tap comfortably.
- VoiceOver labels must include the card category, observed comparison, reporting-period context, and review-oriented caution.
- Mark decorative icons as decorative; otherwise provide equivalent accessible text.
- Present insufficient-data content as information rather than an error.
- Avoid motion in version 1. If motion is added later, respect Reduce Motion.

## Acceptance criteria

- The existing summary list contains exactly one new `AI Usage Insights` row.
- Selecting the row resolves through `DestinationGraph` to exactly one `UsageInsightsView`.
- The screen renders zero to three cards in activity, model-mix, then delivery-context order.
- `UsageInsight` contains no developer names, IDs, ticket titles, prompt content, or other sensitive source data.
- No insight rule makes a network request or runtime LLM call.
- Activity cards require valid, finite, non-negative totals, at least 1,000,000 tokens in both periods, and an unrounded relative change of at least 15%.
- Model-mix cards require positive aggregate totals in both periods and an unrounded absolute share shift of at least 10 percentage points.
- Delivery cards require two complete aggregate periods, a change of at least 5%, and explicit non-causal review copy.
- Missing or invalid data from one source does not suppress valid cards from another source.
- The screen distinguishes insufficient data from no noteworthy patterns.
- Cards, states, and the summary row are usable with Dynamic Type and VoiceOver.
- Automated tests cover threshold boundaries, missing periods, zero totals, invalid numeric values, low volumes, one-period-only models, tied shifts, multiple qualifying shifts, and conflicting signals.

## Open questions

- Confirm the exact sensitive aggregate fields that must be excluded from cards, accessibility labels, and any future drill-downs.
- Decide whether an optional low-emphasis “Explore dashboard trends” action should be added later, only if it fits the existing navigation structure without adding complexity.
