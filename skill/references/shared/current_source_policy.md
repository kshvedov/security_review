# Current Source Policy

Use current-source verification proportionally. Freshness matters most when the decision depends on facts that can change.

## When Current Verification Is Required

Current-source verification is required for:

- Live, time-sensitive, or production-impacting decisions
- Vendor, SaaS, platform, cloud, browser, dependency, package, framework, AI/LLM, agent, CVE, advisory, active-exploitation, or legal/privacy/compliance-sensitive decisions
- Any review where Green depends on current external facts
- Any claim about current provider defaults, current product behavior, current restrictions, current exploitability, current vulnerability status, current guidance, current retention/data-use terms, or current mitigation status

## Stable Principles

For stable design principles, use current checks only when currentness materially affects the decision. Examples of stable principles include server-side authorization, least privilege, evidence minimization, redaction-first reporting, safe logging, and separating severity from confidence.

If the review combines a stable principle with changing external facts, verify the external facts before relying on them.

## Preferred Sources

Prefer authoritative and current sources:

- Official vendor advisories and product documentation
- Official cloud, platform, browser, framework, and SaaS security documentation
- CISA KEV
- NVD/CVE records
- OWASP guidance
- MITRE CWE, CAPEC, and ATT&CK
- Official project release notes or security advisories for dependencies
- Internal owner-confirmed policy or configuration summaries when external publication is not available

Use secondary sources only as supporting context, not as the primary basis for Green on freshness-critical decisions.

## Wording Rules

Do not say a source, framework, advisory, vendor setting, or external status was "checked", "verified", or "confirmed" unless one of these happened in the review:

- A live lookup was performed.
- The user provided the source evidence.
- An owner-confirmed current context was provided.

If no current external verification was performed, say that directly.

Use `Not required for this stable design principle.` for local static-file reviews or stable security principles where current external facts do not affect the decision.

If mentioning general frameworks or public guidance without a live lookup or provided source, describe them as relevant background only, not as checked current-source evidence.

## Recording The Basis

Record one of these in the shared output field:

- The current authoritative source basis checked, when live lookup or provided source evidence was used
- The owner-confirmed current context, when provided
- The current status that could not be verified
- Why current verification was not material for a stable design principle

If current status cannot be safely verified, lower confidence, list the unknown, state the required confirmation, and avoid Green when the current fact is material.

Absence from public advisories, CVE databases, KEV, vendor notices, or public guidance is not proof of safety.
