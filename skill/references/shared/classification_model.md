# Classification Model

Use the same decision color, severity, confidence, and gate result model for Quick, Medium, and Indepth reviews.

## Decision Colors

| Color | Meaning | Use when | Gate impact | Common mistake to avoid |
|---|---|---|---|---|
| Red | Dangerous and blocking. | Confirmed or likely serious risk: exposed real secrets, exposed real sensitive data, authentication or authorization failure, public private data, privileged action to the wrong actor, unsafe production credential use, dangerous cloud or resource exposure, or an action that should not proceed. | Fail. | Do not downgrade Red because exploitation was not demonstrated. |
| Orange | Serious concern requiring owner or technical review before approval. | Serious risk is plausible but needs confirmation: unknown token restrictions, suspicious access boundary, unknown vendor or AI retention, unclear broad permissions, uncertain sensitive staging data, or other sensitive context gap. | Needs escalation. | Do not treat Orange as ticketable Yellow when sensitive context is missing. |
| Yellow | Real issue that should be fixed, ticketed, documented, or accepted. | Low-to-moderate risk, hygiene gap, documentation gap, minor configuration issue, low-risk outdated dependency, non-sensitive debug metadata, or controlled issue with owner and follow-up. | Can pass with ticketing or documented acceptance if no Red, unresolved Orange, or sensitive Gray remains. | Do not use Yellow for unknown sensitive risk. |
| Green | Safe, expected, acceptable, or intentionally public. | Evidence confirms required safe conditions, such as synthetic or redacted data, intentionally public non-sensitive content, documented publishable restricted key, approved vendor integration, confirmed backend enforcement, and current external facts where relevant. | Pass for that item. | Do not classify Green from assumptions or only because harm is unproven. |
| Gray | Unknown or insufficient evidence. | Available evidence cannot safely classify the issue. | Needs more context or escalation. Does not pass if sensitive or critical areas are affected. | Do not turn Gray into Green without explicit safe evidence and current-source support where relevant. |

## Browser-Visible Credential-Like Values

Browser-visible credential-like values are Red/Fail unless the provided evidence clearly documents that the value is fake, public, non-sensitive, and non-usable.

Unknown liveness is not enough to downgrade browser-visible credential-like material to Orange. Do not validate, decode, or test the value. Classify from passive evidence and owner-confirmed context only.

## Green And Partial Safety

Green and Pass must be supported by evidence, not assumptions.

Do not put a required safety condition in `Assumptions` and still mark the item Green or Pass.

If only part of a request is supported as safe:

- Classify that part Green.
- State the boundary clearly.
- Put remaining tool, policy, approval, audience, current-source, or environment gaps in `Unknowns`, `Required Action`, or `Notes`.

For example, generic non-sensitive text may be Green for the content itself, while the user still must use an approved tool or approved workflow.

## Description-Only Green Or Pass

When the user provides a description but the final artifact was not inspected, Green/Pass may apply only to the described scenario.

Use wording such as `Pass for the described page only` or `Green for the described content only`.

If the final artifact matching the description matters, put that boundary in `Unknowns`, `Required Action`, or `Notes`, not `Assumptions`.

Do not treat `the published page matches your description` as an assumption that supports Pass. Treat it as a pre-share check or unknown until the artifact is inspected.

## Severity

Severity is potential impact. It is separate from decision color and confidence.

- Critical: May cause system compromise, account takeover, broad sensitive-data exposure, production compromise, privilege escalation, broad cloud compromise, direct customer harm, serious financial or operational harm, or high-impact business failure.
- High: May expose important data, allow unauthorized actions, weaken key controls, compromise a significant workflow, or create serious operational or security risk.
- Medium: Creates meaningful risk, but impact is limited, scoped, indirect, or requires additional conditions.
- Low: Minor weakness, hygiene concern, low-impact misconfiguration, limited exposure, or documentation gap.
- Informational: Useful to note but not a security issue by itself.

A finding can be Critical severity with Low confidence, Low severity with High confidence, or any other combination. Do not inflate severity just because something looks suspicious. Do not reduce severity only because exploitation was not demonstrated.

## Confidence

Confidence is certainty about the classification. It is separate from severity.

- High confidence: Direct redacted evidence, owner-confirmed implementation context, and relevant current-source verification support the result.
- Medium confidence: Evidence is credible, but scope, sensitivity, reachability, or current platform/vendor status is partly incomplete.
- Low confidence: Evidence is incomplete, indirect, ambiguous, unverified, or depends on current facts that were not confirmed.

Confidence can increase through safe context, owner confirmation, redacted settings, architecture descriptions, current official documentation, synthetic or local examples, and safe scan summaries. Confidence must not be increased by requesting secrets, raw PII, unauthorized tests, live credential validation, or access to data the reviewer does not own.

## Gate Results

| Gate result | Use when | Required action | Evidence needed to clear |
|---|---|---|---|
| Pass | No Red, unresolved Orange, or sensitive/critical Gray remains; Yellow is fixed, ticketed, documented, or accepted; Green is supported by evidence rather than assumptions. | Document result and any ticket or acceptance. | Safe evidence and owner confirmations for relevant conditions. |
| Fail | Any Red finding exists, unsafe evidence handling occurred, or approval depends on unknown critical context. | Stop the action or release, remediate, contain, redact, rotate or revoke where needed, and re-review. | Redacted remediation proof and owner confirmation. |
| Needs escalation | Orange exists or required owner confirmation is missing. | Route to the appropriate owner. | Owner-confirmed controls, sensitivity, scope, approval, and remediation path. |
| Needs more context | Evidence is insufficient and the missing context can be safely provided. | Ask for safe context only. | Redacted evidence, synthetic examples, summaries, or owner statements. |
| Can pass with ticketing | Yellow issue is real but not blocking; owner and follow-up are defined. | Create or reference a ticket with owner, scope, due date, or review cadence. | Ticket or record and no unresolved Red, Orange, or sensitive Gray. |
| Can pass with documented acceptance | Responsible owner accepts known non-Red risk and sensitive unknowns are resolved. | Record owner, rationale, scope, expiry or review cadence, and compensating controls. | Documented acceptance from the responsible owner. |
