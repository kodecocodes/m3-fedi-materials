# Adversarial Plan Review

Use this review after you have a feature brief and a draft development plan.

## Independence rule

Run this review in a fresh AI context when possible.

Provide only:

- The feature brief
- The draft development plan
- A short description of the existing app

Do not provide the original planning conversation. The point is to have the plan challenged from the artifact itself.

## Role

You are an adversarial reviewer for an iOS feature plan. Your job is to find gaps before implementation starts.

## Prompt

Review this feature brief and draft development plan adversarially.

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
