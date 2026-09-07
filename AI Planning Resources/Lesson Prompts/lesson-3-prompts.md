# Lesson 3 Prompts: Challenge and Refine the Plan

Use these prompts during Lesson 3. Start with the `feature-brief.md` and `draft-development-plan.md` files you created in the previous lessons.

## Prompting note

This lesson uses an independent adversarial review. If possible, run all three prompts in a fresh AI chat or session. Do not include the full planning conversation from Lessons 1 and 2. The reviewer should critique the current artifacts, not continue the original conversation.

Paste the two starting artifacts into Prompt 1. After receiving the review, state which findings you accept, reject, want revised, or want to investigate later. Prompt 2 creates `adversarial-review-notes.md` from that review and your decisions. Prompt 3 then creates the complete `reviewed-feature-plan.md`. Keep all three prompts and your review decisions in the same fresh conversation.

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

## Prompt 2: Create the Adversarial Review Notes

```text
Using the adversarial review and my decisions from this conversation, create the complete contents of a file named `adversarial-review-notes.md`.

My decisions stated during the conversation override the AI review.

Rules:
- Record which findings I accepted, rejected, revised, deferred, or chose to investigate later.
- Do not invent decisions I did not make.
- Preserve unresolved findings instead of silently deciding them.
- Keep the distinction between must-fix issues, suggestions, and acceptable tradeoffs.
- Keep the notes concise but specific enough to explain why each decision was made.

Use this structure:

# Adversarial Review Notes: AI Usage Insights

## Review context

## Must fix

For each finding, include:
- Finding
- Why it matters
- Suggested change
- Human decision

## Should consider

For each finding, include:
- Finding
- Why it matters
- Suggested change
- Human decision

## Acceptable tradeoffs

For each tradeoff, include:
- Tradeoff
- Why it may be acceptable
- What to watch during implementation
- Human decision

## Final triage summary

### Accepted changes

### Rejected changes

### Investigate later

### Decisions requiring stakeholder approval

If your environment supports file creation, create or update `adversarial-review-notes.md`. Otherwise, return only the complete Markdown content without introductory commentary.
```

## Prompt 3: Create the Reviewed Feature Plan

Run this prompt after checking `adversarial-review-notes.md` and correcting anything that does not accurately reflect your decisions.

```text
Using the feature brief, draft development plan, adversarial review, adversarial review notes, and my decisions from this conversation, create the complete contents of a file named `reviewed-feature-plan.md`.

My decisions stated during the conversation override earlier AI recommendations.

Rules:
- Apply only findings and recommendations I accepted.
- Do not reintroduce anything I rejected.
- Clearly identify anything deferred from version 1.
- Preserve unresolved decisions under Open Questions.
- Keep the feature team-level.
- Do not expose individual developer names in insight cards.
- Use deterministic local insight rules.
- Do not add runtime LLM calls.
- Do not add networking, persistence, authentication, or a backend.
- Do not add a tab bar or per-insight detail screens.
- Do not claim that AI caused delivery improvements.
- Do not classify models as premium, standard, or cheap.
- Do not include implementation code.
- Keep the plan scoped to a small, realistic version 1.

Use this structure:

# Reviewed Feature Plan: AI Usage Insights

## Feature summary

## Audience

## Goals

## Non-goals

## User flow

## UI plan

## Proposed Swift surface

## Proposed files

## Data flow

## Final version 1 insight rules

## Deferred from version 1

## Edge cases

## Accessibility requirements

## Acceptance criteria

## Open questions

## Final status

If your environment supports file creation, create or update `reviewed-feature-plan.md`. Otherwise, return only the complete Markdown content without introductory commentary.
```
