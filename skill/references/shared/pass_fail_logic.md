# Pass/Fail Logic

Use this gate logic for every review depth.

## Pass

Pass only when all of these are true:

- No Red findings exist.
- No unresolved Orange findings exist.
- No unresolved Gray findings affect sensitive or critical areas.
- Yellow findings are fixed, ticketed, documented, or explicitly accepted by the right owner.
- Green findings are supported by required safe context and current-source verification where currentness is material.
- PII and secrets were handled safely.

## Fail

Fail when any of these are true:

- Any Red finding exists.
- Sensitive data or secrets are exposed unsafely.
- Authentication or authorization is broken in a harmful way.
- Private resources are public without approval.
- Production credentials are exposed or misused.
- The proposed action should not proceed.
- Unsafe evidence handling occurred.
- Approval depends on unknown critical context.

## Needs Escalation

Needs escalation when any Orange finding is unresolved, required owner confirmation is missing, or Gray affects:

- Sensitive data
- Credentials
- Production systems
- Cloud or platform exposure
- Access control
- External sharing
- Privileged actions
- Customer impact
- AI or automation action
- Legal/privacy/compliance-sensitive areas

Name the owner and the exact safe confirmation needed.

## Needs More Context

Needs more context when evidence is insufficient and the missing context can be safely provided without secrets, raw PII, private screenshots, live links, unsafe validation, unauthorized access, or unsafe proof.

Ask for redacted evidence, synthetic examples, safe summaries, public documentation, owner statements, or current-source basis.

## Can Pass With Ticketing

Can pass with ticketing only when a Yellow issue is real but not blocking, an owner and follow-up are defined, and no Red, unresolved Orange, or sensitive Gray remains.

The ticket or tracking record should include owner, scope, required action, due date or review cadence, and any compensating controls.

## Can Pass With Documented Acceptance

Can pass with documented acceptance only when the responsible owner accepts a known non-Red risk, the acceptance is documented with scope and review cadence, and sensitive Gray unknowns are resolved first.

Documented acceptance should include owner, rationale, scope, expiration or review cadence, compensating controls, and re-review trigger.

## Gate Explanation

Every review should explain the gate result by tying it to:

- Decision color
- Severity
- Confidence
- Evidence
- Unknowns
- Current-source status where relevant
- Required owner confirmation or remediation
