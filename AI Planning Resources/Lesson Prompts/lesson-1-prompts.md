# Lesson 1 Prompts: Shape the Feature

Use these prompts during Lesson 1. The responses from your AI tool may not match the video exactly, and that is expected. Focus on the review workflow and the decisions you make from the responses.

## Prompting note

These prompts are longer than a quick chat message on purpose. Planning prompts work better when the model has enough context to understand:

- what the app already does,
- who the feature is for,
- what decisions are already made,
- what the feature should avoid,
- and what format you want back.

You can use these prompts with any capable AI assistant, including ChatGPT, Claude, Gemini, Cursor, Codex, or another tool that can work with project context and Markdown. The exact wording of the response will vary by tool and model.

## How to use these prompts

The prompts below are complete and ready to paste into your AI tool. You do not need to configure a custom agent, install a skill, or attach the separate role-review files.

The `product-lead-review.md`, `designer-review.md`, and `engineering-manager-review.md` files are reusable reference guides. Each prompt below already adapts the appropriate guide with the Tokens Dashboard context, feature constraints, review focus, and requested response format.

After each AI review, decide which suggestions you accept, reject, or want revised, and state those decisions in the conversation. The review responses are input, not the finished feature brief. After all three reviews, use Prompt 4 to create the complete `feature-brief.md` from your approved decisions.

Run all four prompts in the same conversation so Prompt 4 can use the preceding reviews and your decisions. The `feature-plan-template.md` and `human-review-checklist.md` files are used in later lessons, not in Lesson 1.

## Prompt 1: Product Lead Review

```text
Review this feature idea as a product lead.

App context:
Tokens Dashboard is a small SwiftUI app that shows AI usage and delivery metrics for a software team. It currently has a summary screen and detail screens for cost by model, tokens versus outcomes, and ticket-to-merge trends.

Rough feature idea:
Add AI Usage Insights to the Tokens Dashboard so a team lead can understand team-level AI usage patterns.

Target audience:
Team leads, engineering managers, and project leads who need to review team-level AI usage and delivery patterns.

Known constraints:
- Keep the feature team-level.
- Do not expose individual developer names in insight cards.
- Do not use an LLM inside the app at runtime.
- Do not tell people to "use more AI."
- Do not claim that AI caused delivery improvements.
- Do not make real-world pricing or premium-model assumptions.
- Keep v1 small enough to plan clearly.

Focus on:
- Who this feature is for
- What user problem it solves
- What decision or workflow it improves
- What the smallest useful version should include
- What should be excluded from v1
- What could make the feature confusing, misleading, or harmful
- What assumptions need human confirmation

Return:
1. A short product framing
2. A proposed v1 scope
3. Non-goals
4. Risks and weak assumptions
5. Questions the developer should answer before planning implementation

Do not write code. Do not expand the feature beyond the app and audience described.
```

## Prompt 2: Designer Review

```text
Review this feature as a product designer.

App UI context:
Tokens Dashboard is a SwiftUI app with a narrative summary screen. The summary screen lists short insight-style rows, and each row navigates to a detail chart screen. Existing detail screens show cost by model, tokens versus outcomes, and ticket-to-merge trends.

Feature brief so far:
AI Usage Insights helps a team lead, engineering manager, or project lead review team-level AI usage patterns without overreacting to raw metrics. The feature should turn selected chart patterns into cautious review prompts.

Constraints:
- Keep the existing summary-to-detail navigation style.
- Keep the feature team-level.
- Do not expose individual developer names in insight cards.
- Do not create a tab bar.
- Do not create per-insight detail screens for v1.
- The copy should be cautious, not accusatory.
- The UI should make clear that insights are review prompts, not automatic conclusions.

Focus on:
- Where the feature should live in the current app
- What the primary user flow should be
- What information belongs on screen
- What information should be hidden, shortened, or deferred
- How to avoid accusatory or overconfident language
- How to show uncertainty or caution without making the UI feel useless
- What accessibility concerns should be planned now

Return:
1. Recommended user flow
2. Recommended screen structure
3. Content hierarchy for the main UI
4. Copy risks and wording guidelines
5. Accessibility notes
6. Design decisions that need human approval

Do not create a large redesign unless the current app structure cannot support the feature.
```

## Prompt 3: Engineering Manager Review

```text
Review this feature as an engineering manager.

Feature brief:
AI Usage Insights adds one new summary row and one new insights screen to the Tokens Dashboard app. It surfaces cautious team-level review signals from existing mock data. The app does not call an LLM at runtime.

Relevant app architecture:
- SwiftUI app.
- `SummaryView` shows summary rows and uses navigation destinations.
- `SummaryViewModel` builds the current summary rows.
- Existing mock stores include `ModelCostStore`, `DeveloperOutcomeStore`, and `TicketToMergeStore`.
- Existing detail screens include cost by model, tokens versus outcomes, and ticket-to-merge trends.

Known decisions:
- One new summary row.
- One new `UsageInsightsView`.
- Compact insight cards.
- Deterministic local rules.
- No tab bar.
- No per-insight detail screens in v1.
- No individual developer names in insight cards.
- No runtime LLM calls.
- No premium-model or real-world pricing assumptions.

Focus on:
- The smallest useful implementation
- Existing code that should be reused
- New files or types that are likely needed
- Data flow through the app
- API or model surface
- Edge cases that should be planned before implementation
- Testing or validation concerns
- Scope creep to avoid

Return:
1. A recommended implementation shape
2. Files likely to add
3. Files likely to modify
4. Proposed data flow
5. Edge cases
6. Acceptance criteria
7. Open questions that need human review

Do not write the implementation. Keep the plan compatible with the existing app unless there is a clear reason to change the architecture.
```

## Prompt 4: Create the Feature Brief

Run this prompt after completing the product lead, designer, and engineering manager reviews. Before using it, make sure you have stated which recommendations you accept, reject, or want revised after each review.

```text
Using the product lead, designer, and engineering manager reviews from this conversation, create the complete content for a file named `feature-brief.md`.

The decisions I made after each review override any earlier AI recommendations.

Rules:
- Include only ideas and recommendations I accepted.
- Do not reintroduce anything I rejected.
- Preserve unresolved decisions as open questions.
- Keep the feature team-level.
- Do not include individual developer names.
- Do not add runtime LLM calls, networking, authentication, persistence, or backend services.
- Do not claim that AI usage caused delivery improvements.
- Do not make pricing or premium-model assumptions.
- Do not include implementation code.
- Keep the feature scoped to a small, realistic version 1.

Use this structure:

# Feature Brief: AI Usage Insights

## Feature name

## Rough idea

## Audience

## Problem statement

## UI direction

## Version 1 scope

## Non-goals

## Initial insight candidates

## Human-review constraints

## Open questions

Return only the complete Markdown content for `feature-brief.md`, without introductory commentary.
```
