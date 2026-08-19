# Lesson 3 Prompts: Challenge and Refine the Plan

Use these prompts during Lesson 3. Start with the `feature-brief.md` and `draft-development-plan.md` files you created in the previous lessons.

## Prompting note

This lesson uses an independent adversarial review. If possible, run Prompt 1 in a fresh AI chat or session. Do not include the full planning conversation from Lessons 1 and 2. The reviewer should critique the current artifacts, not continue the original conversation.

## Prompt 1: Adversarial Plan Review

```text
Review this feature brief and draft development plan adversarially.

Feature brief:
[Paste your feature-brief.md content here]

Draft development plan:
[Paste your draft-development-plan.md content here]

Existing app context:
Tokens Dashboard is a small SwiftUI app with a summary screen and detail chart screens. It uses fixed mock data for model cost, developer outcomes, and ticket-to-merge trends. This exercise focuses on producing and reviewing a development plan. Do not implement the feature or write production code.

Look for:
- Weak assumptions
- Missing edge cases
- Unclear API or data boundaries
- UI complexity that does not serve the user
- Product language that overclaims or sounds too confident
- Privacy or safety risks
- Places where the plan implies causation from correlation
- Scope creep
- Simpler alternatives
- Decisions that should be made by a human, not guessed by AI

Return findings in this format:

## Must fix

- Finding:
- Why it matters:
- Suggested change:

## Should consider

- Finding:
- Why it matters:
- Suggested change:

## Acceptable tradeoffs

- Tradeoff:
- Why it may be acceptable:
- What to watch during implementation:

## Questions for the human reviewer

- Which findings are must-fix issues before implementation?
- Which findings are acceptable tradeoffs for v1?
- Which findings should be deferred because they would expand the feature too much?
- Which decisions require product, design, or stakeholder approval?
- Does the final plan still match the original feature goal?

Do not rewrite the full plan. Critique it first. The human reviewer will decide what to accept, reject, or investigate later.
```

## Prompt 2: Apply Accepted Review Decisions

```text
Update this draft development plan using only the accepted human review decisions below.

Draft development plan:
[Paste your draft-development-plan.md content here]

Accepted decisions:
[Paste the decisions you accepted from adversarial-review-notes.md]

Rules:
- Do not add new scope beyond the accepted decisions.
- Keep the feature team-level.
- Do not expose individual developer names in insight cards.
- Do not add runtime AI calls.
- Do not add networking, persistence, authentication, or a backend.
- Do not claim that AI caused delivery improvements.
- Do not classify models as premium, standard, or cheap.
- Keep unresolved questions clearly marked.

Return a revised plan using this structure:
1. Feature summary
2. Audience
3. Goals
4. Non-goals
5. User flow
6. UI plan
7. Proposed Swift surface
8. Proposed files
9. Data flow
10. Final v1 insight rules
11. Deferred from v1
12. Edge cases
13. Accessibility requirements
14. Acceptance criteria
15. Open questions
16. Final status
```
