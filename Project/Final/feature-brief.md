# Feature Brief: AI Usage Insights

## Feature name

AI Usage Insights

## Rough idea

Add one AI Usage Insights row to the existing Tokens Dashboard summary screen. Selecting the row opens one insights screen with compact, team-level cards that turn existing mock-data patterns into cautious prompts for review.

## Audience

Team leads, engineering managers, and project leads reviewing team-level AI usage and delivery patterns.

## Problem statement

Leads need a concise way to notice meaningful team-level AI usage patterns without overreacting to raw metrics or drawing causal conclusions about delivery. The feature provides aggregate context to support planning and retrospective conversations.

## UI direction

Preserve the app’s existing summary-to-detail navigation pattern:

1. The existing narrative summary screen includes one new `AI Usage Insights` row.
2. Selecting the row opens one `UsageInsightsView`.
3. The insights screen shows up to three compact insight cards.
4. Cards are informational in version 1; they do not have individual detail destinations.
5. An optional low-emphasis “Explore dashboard trends” action may appear at the bottom if it fits the existing navigation structure easily.

The insights screen should clearly describe cards as team-level review prompts, not automatic conclusions.

## Version 1 scope

- One new summary row: `AI Usage Insights`.
- One new insights screen: `UsageInsightsView`.
- Up to three compact, aggregate insight cards.
- Deterministic local rules based on existing mock data.
- Use the existing reporting period and compare it with the immediately preceding equal-length period.
- Surface a trend when the relative change reaches 15% and both comparison periods have sufficient data.
- Suppress percentage-based insights when the prior period is zero or below a configurable minimum volume.
- Show a clear insufficient-data state when comparison data is unavailable.
- Use a stable card order:
  1. AI activity
  2. Model mix
  3. Delivery context
- Keep calculation rules separate from SwiftUI presentation so they can be tested independently.
- Use only aggregate, display-ready data in insight-card models.

## Non-goals

- Individual developer names, records, rankings, or surveillance.
- Per-insight detail screens.
- A tab bar or broader navigation redesign.
- Runtime LLM calls.
- Networking, authentication, persistence, or backend services.
- Recommendations to use more AI.
- Claims that AI usage caused delivery improvements.
- Pricing advice, premium-model recommendations, or real-world pricing assumptions.
- Forecasting, benchmarking, alerting, anomaly detection, or automated interventions.

## Initial insight candidates

### AI activity changed

Show a period-over-period change in aggregate team token activity.

Example wording:

> Team token activity increased 18% compared with the prior period.
> Review alongside current project and delivery context.

### Model mix shifted

Show a meaningful shift in the team’s aggregate usage distribution by model.

Example wording:

> A larger share of team usage came from Model A this period.
> Review whether this reflects the team’s current work.

### Delivery trend changed

Show a change in existing aggregate ticket-to-merge timing alongside the same reporting period.

Example wording:

> Ticket-to-merge time changed during the same period.
> This is context for review, not evidence of cause.

## Human-review constraints

- Keep all insights at the team level.
- Do not show individual developer names or sensitive information.
- Use neutral, observed facts before review prompts.
- Do not assign motive, performance, quality, or causality.
- Do not use warning language, urgency colors, grades, scores, rankings, or “good” versus “bad” trend treatment.
- Do not rely on color or direction icons alone; provide text equivalents.
- Support Dynamic Type, adequate contrast, large tap targets, and clear VoiceOver labels.
- Present unavailable or insufficient data as a clear informational state rather than an error.

## Open questions

- What exact aggregate fields count as sensitive information and must be excluded from cards, accessibility labels, and any future drill-downs?
- What configurable minimum volume should suppress percentage-based comparisons for the existing mock datasets?
- Does the optional “Explore dashboard trends” action fit the current navigation structure without adding complexity?
