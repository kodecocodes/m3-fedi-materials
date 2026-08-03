# Lesson 2 Prompts: Create the Development Plan

Use these prompts during Lesson 2. Start with the `feature-brief.md` file you created in Lesson 1.

## Prompting note

This lesson turns a feature brief into an iOS development plan. The prompts are intentionally specific because the goal is not a generic feature brainstorm. The goal is a plan that fits the existing Tokens Dashboard app.

If your AI tool can see the project files, include the relevant files or project context. If it cannot, paste the architecture summary from the lesson.

## Prompt 1: Draft the iOS Development Plan

```text
Create an iOS development plan from this feature brief.

Feature brief:
[Paste your feature-brief.md content here]

App architecture context:
- Tokens Dashboard is a small SwiftUI app.
- `SummaryView` shows a narrative summary list and uses `NavigationStack`.
- `DestinationGraph` controls the existing navigation destinations.
- `SummaryViewModel` builds summary rows.
- Existing stores include `ModelCostStore`, `DeveloperOutcomeStore`, and `TicketToMergeStore`.
- Existing views include `CostbyModelView`, `TokensOutcomesView`, and `TicketToMergeView`.
- Existing view models format chart data for the views.
- The app uses fixed mock data, not networking.

Planning constraints:
- Do not write implementation code.
- Do not add an LLM call inside the app.
- Do not add networking, persistence, authentication, or a backend.
- Do not add a tab bar.
- Do not add per-insight detail screens in v1.
- Keep the feature team-level.
- Do not expose individual developer names in insight cards.
- Do not claim that AI caused delivery improvements.
- Do not classify models as premium, standard, or cheap.
- Keep the plan small enough for a later implementation pass.

Use this structure:
1. Feature summary
2. Goals
3. Non-goals
4. User flow
5. UI plan
6. Proposed Swift surface
7. Proposed files
8. Data flow
9. Insight rules
10. Edge cases
11. Accessibility requirements
12. Acceptance criteria
13. Open questions

Be specific enough that a developer or AI coding agent could implement the plan later, but do not write the feature code.
```

## Prompt 2: Review API Surface and Edge Cases

```text
Review this draft development plan for iOS implementation readiness.

Draft development plan:
[Paste your draft-development-plan.md content here]

Focus on:
- Whether the proposed Swift types are clear enough
- Whether the data flow is explicit
- Whether the rules are deterministic
- Whether the plan avoids runtime AI calls
- Whether the plan avoids individual-level performance judgment
- Missing edge cases
- Missing accessibility requirements
- Acceptance criteria that are too vague
- Open questions that should be marked before implementation

Return:
1. API surface issues
2. Missing or unclear data flow
3. Edge cases to add
4. Accessibility improvements
5. Acceptance criteria improvements
6. Human decisions that should remain open

Do not rewrite the whole plan. Give targeted improvements.
```

