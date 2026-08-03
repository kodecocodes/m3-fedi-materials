# Human Review Checklist

Use this checklist after the adversarial review. The AI reviewer can find useful issues, but the human developer owns the final plan.

## Review every finding

For each adversarial finding, mark one:

- Accept
- Reject
- Investigate later

## Product checks

- [ ] The feature still solves the original user problem.
- [ ] The audience is clear.
- [ ] The v1 scope is small enough to implement.
- [ ] The plan avoids unnecessary product expansion.
- [ ] Any unresolved product decisions are marked as open questions.

## Design checks

- [ ] The user flow fits the existing app.
- [ ] The UI hierarchy is not too text-heavy.
- [ ] The copy is cautious and useful.
- [ ] The UI does not imply more certainty than the data supports.
- [ ] The plan includes accessibility requirements.

## Engineering checks

- [ ] The planned files and types fit the existing architecture.
- [ ] The data flow is explicit.
- [ ] Business logic is deterministic and explainable.
- [ ] Edge cases are listed.
- [ ] Acceptance criteria are testable.
- [ ] The plan does not include implementation code.

## Responsible-use checks

- [ ] The plan does not expose individual developer names in team-level insights.
- [ ] The plan does not use token volume alone as a performance signal.
- [ ] The plan does not claim AI caused a delivery improvement.
- [ ] The plan does not assume model pricing or premium tiers unless that metadata exists.
- [ ] The plan clearly separates review signals from automatic conclusions.

## Final plan status

Mark the final reviewed plan as one:

- Ready for implementation
- Ready with open questions
- Needs another planning pass

