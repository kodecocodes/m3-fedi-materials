# Adversarial Review Notes: AI Usage Insights

## Review context

The feature adds an `AI Usage Insights` row and an insights screen to a small SwiftUI prototype using fixed mock data. The review focused on preserving team-level, non-causal, privacy-conscious review prompts. The human reviewer accepted all fixes identified in the adversarial review. Defaults and recommendations offered for open questions are recorded as recommendations, not as final human decisions.

## Must fix

### Finding

The proposed delivery-context input is not a true team-level metric: it is derived from separate “Heavy AI users” and “Light AI users” cohort averages, with no cohort sizes.

### Why it matters

An equal-weighted average could misrepresent team delivery timing, expose a sensitive AI-usage grouping, and invite causal interpretations.

### Suggested change

Exclude the delivery-context card from v1. Reconsider it only when a valid, period-aligned team-level metric and population counts are available.

### Human decision

Accepted. Delivery context is out of v1 under the current data model.

### Finding

The token and delivery sources use inconsistent reporting periods; token data is month-to-date while delivery data is monthly.

### Why it matters

Different or incomplete windows make comparisons misleading.

### Suggested change

Define one explicit period contract: equal-length completed windows, reporting timezone, start and end timestamps, and completeness rules. Suppress comparisons that do not meet it.

### Human decision

Accepted.

### Finding

Adding `previousTokens` to the current `ModelCost` model creates an unclear historical-data boundary.

### Why it matters

It leaves historical-period semantics, missing-model behavior, and stable model identity ambiguous.

### Suggested change

Use a period-based aggregate input model with period metadata and stable model identifiers.

### Human decision

Accepted.

### Finding

“No noteworthy patterns” can overstate what threshold-based rules establish.

### Why it matters

It could be understood as assurance that no meaningful issue exists.

### Suggested change

Use the more precise state copy: “No changes met the current review thresholds for this period.”

### Human decision

Accepted.

## Should consider

### Finding

Aggregate data can still expose sensitive behavior for small teams or narrow periods.

### Why it matters

Model usage, costs, or time periods may reveal sensitive team strategy or activity even without individual records.

### Suggested change

Define a privacy floor and permitted fields. The review recommended a minimum group size of 10, with no individual fields, costs, prompts, ticket titles, or cohort labels.

### Human decision

Accepted as a required safeguard. The exact privacy floor and permitted fields remain unresolved and require stakeholder approval; the group-size value of 10 is a recommendation, not a recorded decision.

### Finding

The plan does not state how partial source availability is communicated when one or more cards remain valid.

### Why it matters

A partial screen could appear complete.

### Suggested change

Show a brief neutral coverage note when categories could not be compared, for example: “Some insight categories could not be compared for this period.”

### Human decision

Accepted.

### Finding

Existing summary content contains individual rankings and strong AI-to-delivery causal language that conflicts with the new feature’s team-level, cautious intent.

### Why it matters

The new feature would sit beside contradictory and potentially unsafe claims.

### Suggested change

Track correction of existing summary content as a separate safety follow-up before broader release; do not silently treat the overall summary screen as compliant.

### Human decision

Accepted as a separate safety dependency. Its scope, owner, and timing remain unresolved.

## Acceptable tradeoffs

### Tradeoff

Limit v1 to one screen with up to two cards: AI activity and model mix.

### Why it may be acceptable

It fits the available aggregate mock data and keeps the feature compact and testable.

### What to watch during implementation

Do not add drill-downs, alerts, forecasting, or an exploratory dashboard action without a validated user need.

### Human decision

No explicit decision recorded. This remains a recommendation consistent with excluding delivery context from v1.

### Tradeoff

Use deterministic local rules and fixed mock data.

### Why it may be acceptable

It is transparent, testable, and avoids network, identity, and automated-decision risks.

### What to watch during implementation

Keep thresholds configurable and describe outputs as review prompts rather than conclusions.

### Human decision

No explicit decision recorded. This remains the proposed v1 approach.

### Tradeoff

Show only the largest qualifying model-share shift.

### Why it may be acceptable

It keeps the model-mix card compact and easy to scan.

### What to watch during implementation

Identify it as the largest observed share shift, include the percentage-point change, and do not imply that a model is better, worse, or recommended.

### Human decision

No explicit decision recorded. This remains a recommendation.

## Final triage summary

### Accepted changes

- Exclude delivery context from v1 until valid team-level, period-aligned delivery data is available.
- Define a consistent, completed reporting-period contract.
- Replace embedded prior-token fields with a period-based aggregate input boundary.
- Replace “No noteworthy patterns” with threshold-specific, non-assuring copy.
- Add privacy safeguards, while leaving their exact policy for approval.
- Make partial comparison coverage visible.
- Treat correction of conflicting existing summary language as a separate safety dependency.

### Rejected changes

No findings or suggestions were explicitly rejected.

### Investigate later

- Whether delivery context can return after a valid team-level data source, period alignment, and population counts exist.
- The exact minimum group size and permitted aggregate fields.
- Ownership, scope, and timing for correcting existing summary content.
- Whether to add drill-downs, dashboard exploration, alerts, forecasting, or richer model-distribution views after v1.
- Whether one representative model-mix shift is sufficient for the user’s review task.

### Decisions requiring stakeholder approval

- Product approval of insight thresholds, the final v1 card set, and the product meaning of “notable” changes.
- Design approval of neutral state copy, partial-coverage presentation, and accessibility treatment.
- Privacy or stakeholder approval of the minimum group size, allowed aggregate fields, and whether model names, costs, or reporting periods are sensitive.
- Approval of the scope and release criteria for correcting existing summary-screen individual rankings and causal claims.
