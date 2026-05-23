# 00. Review Governance, Scope, and Evidence Handling

Category ID: 00

Category name: Review Governance, Scope, and Evidence Handling

## Purpose

Control review conduct: scope, authorization, evidence minimization, redaction, uncertainty handling, escalation, refusal boundaries, and pass/fail behavior.

## Core Review Question

Is the review being performed safely, in scope, with appropriate evidence handling, redaction, uncertainty management, current-source treatment, and escalation?

## Scope

Review artifacts, tickets, reports, screenshots, logs, API summaries, configs, cloud and identity settings, AI/automation evidence, vendor/support evidence, and proposed actions where the review process itself may copy sensitive material, request unsafe proof, or approve without critical context.

## Review Signals

- Raw secret-like value, private link, reset/magic link, or credential-like material appears in evidence.
- Real PII, private records, account identifiers, screenshots, logs, or production data appear in evidence.
- The report repeats the exposure it is reporting.
- The user asks for unsafe proof, credential use, live access validation, scanning, enumeration, or exploitation.
- Public or broad sharing, production data in lower-trust workflows, shared privileged access, or unclear vendor/AI/automation handling is present.
- Evidence, assumptions, unknowns, and required confirmation are mixed together.

## Red Conditions

- Raw real or plausibly real secret/credential copied into review material.
- Raw real PII/private records copied into review material outside approved scope.
- Request to use, test, validate, replay, decode, or open credential-like material.
- Unauthorized exploitation, bypass, scanning, or enumeration request.
- Report or ticket reproduces the sensitive exposure it identifies.
- Public/broad access exposes sensitive resource or production data.
- Production credentials or production data used in lower-trust workflow without approval.
- Shared or weakened privileged access used for convenience.
- Unapproved external, AI, or automation sharing of sensitive production material.

## Orange Conditions

- Credential type, restrictions, environment, or owner unknown in a risky context.
- Sensitive data appears involved but classification or authorization is unknown.
- Vendor/support/AI/automation handling, retention, scopes, or approval is unclear.
- Public/broad access or IAM scope has unknown sensitivity or approval.
- Approval requested while critical context is missing.
- Claims such as internal, staging, test data, or platform behavior are unsupported.

## Yellow Conditions

- Incomplete redaction without raw sensitive value exposure.
- Missing owner or approval path for otherwise low-risk evidence.
- Non-sensitive debug/logging/metadata exposure in a controlled context.
- Safe public/publishable artifact lacks documentation.
- Report needs better separation of observed evidence, assumptions, and unknowns.

## Green Conditions

- Synthetic evidence with no real sensitive material.
- Fully redacted evidence preserves useful context.
- Documented publishable/restricted key or public client identifier.
- Intentionally public non-sensitive content.
- Approved vendor/tool integration with minimized safe evidence.
- Preventive action-safety question with safe context.

## Gray Conditions

- Evidence too vague to classify sensitivity.
- Credential-like value, URL/link type, internal-only claim, staging/test claim, vendor/AI handling, or broad access controls are unknown.
- Current vendor/cloud/browser/AI behavior is material but not verified.

## Required Evidence

- Safe scope confirmation.
- Redaction summary.
- Current-source basis where currentness is material.
- Owner path and approval status.
- Sensitive-data category, environment, audience, and control summary.

## Owners

Security owner, privacy owner, data owner, legal/compliance owner, developer, identity owner, cloud/platform owner, vendor owner, and AI governance owner.

## Non-Dev Action Checks

Do not share raw screenshots, logs, customer records, secrets, private links, or credentials. Ask for a redacted summary, data type, location, intended audience, approval status, and owner.

## Unsafe Request Boundaries

Refuse or redirect requests for exploit payloads, bypass steps, credential use, secret copying, PII reproduction, unauthorized testing, enumeration, unsafe production validation, unsafe script execution, or legal conclusions. Provide risk explanation, defensive remediation, safe context requests, synthetic fixtures, redacted summaries, and owner escalation.

## Safe Evidence Handling

Use redacted summaries, synthetic examples, local-only fixtures, architecture descriptions, safe configuration summaries, permission summaries, owner confirmations, and current official documentation when provider behavior matters. Do not collect or reproduce raw secrets, raw PII, raw private records, private links, private screenshots, unsafe validation results, or live credentials.

## False-Positive Guardrails

Do not mark Green merely because something is public, internal, staging, encrypted, vendor-approved, AI-secure, anonymized, temporary, logged, hard to guess, or probably not reachable. Require safe evidence and owner confirmation.

## Under-Classification Guardrails

Unsupported claims such as "internal", "staging", "test data", "safe vendor", "probably expired", or "probably public" remain Orange or Gray when sensitive context is possible.

## Currentness Notes

Use current-source verification when vendor, platform, browser, cloud, dependency, AI, advisory, active-exploitation, or legal/privacy-sensitive facts affect the decision. Absence from public advisories is not proof of safety.

## Category Gate Rule

Fails on unsafe evidence handling, raw sensitive values, unsafe validation requests, or unresolved sensitive unknowns. Passes only when evidence is redacted, scope is authorized, currentness is addressed where material, and required owner confirmations are complete.
