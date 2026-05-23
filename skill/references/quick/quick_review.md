# Quick Review

Quick mode is for simple action-safety checks, short first-pass reviews, and concise triage. It should be fast, safe, and practical.

Use this file with the shared references:

- `../shared/output_format.md`
- `../shared/universal_safety_rules.md`
- `../shared/classification_model.md`
- `../shared/current_source_policy.md`
- `../shared/redaction_and_unsafe_requests.md`
- `../shared/pass_fail_logic.md`
- `../shared/style_policy.md`

Do not redefine the shared output format here. Use `../shared/output_format.md` for every Quick result.

## Quick Scope

Use Quick when the user asks for a quick, simple, brief, or first-pass review, or when the request is a simple action-safety check with limited context.

Escalate to Medium or Indepth when the request needs detailed category rules, code/config review, multiple categories, production impact, secrets, PII, auth/authz, cloud/IAM, CI/CD, AI agents, vendor exposure, broad permissions, customer data, or legal/privacy-sensitive unknowns.

Do not infer whether the user is technical or non-technical. Use the requested style. If no style is specified, use clear, plain, precise language.

## Quick Output Density

Quick output is concise triage. Use the same shared output sections, but keep each section short.

- Name the decision and top 1-3 material reasons.
- Include only representative evidence needed to justify the decision.
- Give the immediate safe action or owner escalation.
- Name browser-visible hidden state as a top-risk family when it changes the sharing decision.
- Do not create a full inventory, category-by-category report, or exhaustive remediation plan.
- If many issues exist, summarize the highest-risk families and recommend Medium or Indepth for fuller coverage.

## Quick Process

1. Identify whether the request is Technical Review Mode or Action Safety Mode.
2. Read the shared files needed for safety, classification, current-source policy, redaction, pass/fail logic, and style.
3. Select the most likely primary category and any useful secondary category.
4. Classify with decision color, severity, confidence, and gate result as separate fields.
5. Ask only for safe context when needed.
6. Provide a safer alternative or owner escalation when the action should not proceed as described.
7. Use the shared output format from `../shared/output_format.md`.

## Direct Action-Safety Behavior

When the user asks whether they can do something safely, answer directly before adding detail:

- Use "Do not proceed as described" for Red or clearly unsafe actions.
- Use "Proceed only if these conditions are confirmed" for Orange, Gray, or context-dependent actions.
- Use "This looks acceptable based on the provided safe context" only when Green is supported by safe evidence and any material current-source needs are satisfied.
- Use "This can proceed with ticketing or documented acceptance" only when the shared pass/fail rules allow it.

## Quick Green Boundary

Green may apply only to the content or action directly supported by safe evidence.

Do not put a required safety condition in `Assumptions` and still mark the item Green or Pass.

If only the provided content is safe, but the tool, policy, approval, audience, or environment is unknown:

- Mark Green only for the provided content itself.
- Put the remaining boundary in `Unknowns`, `Required Action`, or `Notes`.
- Use wording such as: "Green for the provided generic text itself; use only an approved tool or approved workflow."

Ask only for safe context such as:

- Is the data synthetic, redacted, public, or production-derived?
- Who owns the system, data, credential, integration, or workflow?
- Is there approval, expiry, logging, retention, and revocation?
- Is access read-only or write-capable?
- Are MFA, named accounts, least privilege, and audit logs in place?
- What current authoritative source or owner-confirmed setting supports the claim?

Never ask for raw keys, tokens, passwords, PII, private screenshots, live links, production records, exploit proof, unsafe validation output, or credential testing.

## Quick Classification Shortcut

Use `../shared/classification_model.md` as the authority for Red, Orange, Yellow, Green, Gray, severity, confidence, and gate result. In Quick mode, apply the shared model briefly and avoid adding category detail unless it changes the decision, owner routing, or safer alternative.

## Compact Category Selector

Use the primary category for the main failure mode. Add secondary categories only when they improve owner routing, risk explanation, or remediation.

| ID | Category | Use for quick triage |
|---|---|---|
| 00 | Review Governance, Scope, and Evidence Handling | Authorization, scope, redaction, unsafe evidence, current-source basis, escalation, or refusal boundaries. |
| 01 | Identity, Authentication, and Session Trust | Login, MFA, recovery, sessions, cookies, tokens, SSO, service identities, support/vendor access, or auth logs. |
| 02 | Authorization, Access Control, and Trust Boundaries | Server-side authorization, tenant/object access, RBAC/ABAC/ReBAC, ACLs, shared links, revocation, or support/vendor/AI reach. |
| 03 | Sensitive Data, PII, and Privacy Boundaries | Customer, employee, production, confidential, private, exported, logged, shared, retained, or AI/vendor-processed data. |
| 04 | Secrets, Credentials, and Key Management | API keys, tokens, passwords, private keys, connection strings, signed URLs, service accounts, CI/CD/cloud credentials, or rotation. |
| 05 | Input, Query, and Execution Safety | Untrusted input affecting queries, commands, scripts, rendering, redirects, destinations, paths, templates, parsers, or generated output. |
| 06 | API, Service, and Integration Boundaries | APIs, webhooks, callbacks, service scopes, schemas, response shaping, limits, logs, connectors, vendor/no-code/AI integrations. |
| 07 | Client-Side, Browser, and Frontend Exposure | Browser-visible code/data, storage, cookies, headers, source maps, tag managers, analytics, replay, widgets, or frontend-only controls. |
| 08 | File, Object, Content, and Storage Handling | Uploads, downloads, files, reports, backups, buckets, object ACL/IAM, signed links, previews, conversion, CDN/cache, or file vendors. |
| 09 | Business Logic, Abuse Prevention, and Resource Controls | Workflow abuse, approvals, state, quotas, payments/refunds/discounts, bulk actions, messaging, rate limits, cost controls, or overrides. |
| 10 | Configuration, Platform, Cloud, and Deployment Exposure | Cloud/platform/IaC/Kubernetes/Docker/serverless settings, exposure, debug/admin surfaces, CORS, DNS, CDN, IAM, deployments, or drift. |
| 11 | Dependencies, Build, CI/CD, and Supply Chain Integrity | Dependencies, lockfiles, registries, SCA/SBOM, build scripts, CI/CD permissions/secrets, artifacts, releases, runners, or generated code. |
| 12 | Cryptography, Transport, and Data Protection Controls | TLS, HTTPS, certificates, encryption, password hashing, randomness, signing, KMS/key lifecycle, masking, deletion, or vendor encryption claims. |
| 13 | Runtime, Memory, and Program Safety | Native/unsafe code, parsers, converters, workers, scripts, plugins, temp files, sandboxing, resource limits, concurrency, or runtime dependencies. |
| 14 | Logging, Monitoring, Auditability, and Incident Readiness | Logs, dashboards, traces, SIEM/SOC alerts, runbooks, retention, access, integrity, redaction, and attribution for sensitive actions. |
| 15 | AI, Automation, and Agentic-System Safety | AI tools, agents, RAG/vector stores, prompts, memory, tool calls, generated artifacts, no-code/RPA, connectors, approval gates, and AI logs. |

## Common Quick Routing Shortcuts

- Secret in frontend: primary 04, secondary 07.
- PII in logs: primary 03, secondary 14.
- Public bucket or file with customer data: primary 08 or 10, secondary 03 and 02.
- AI tool with CRM/API access: primary 15, secondary 02, 03, 06, and 04.
- API returns excessive sensitive data: primary 06, secondary 03 and 02.
- Shared admin accounts: primary 01, secondary 02 and 14.
- Source maps exposing secrets: primary 11 or 07, secondary 04 and 10.
- Broad vendor integration: primary 06, secondary 02, 04, and 15 when AI/no-code is involved.
- Production data in staging or demo: primary 03 or 10, secondary 02 and 08.
- No-code automation using personal admin credentials: primary 15, secondary 01, 04, and 06.
- AI-generated code in production: primary 15 or 11, secondary 05 and 13.
- Debug mode in production: primary 10, secondary 14, 03, and 04.
- Reachable production dependency vulnerability: primary 11, secondary 13 and 10.

## Compact Category Guidance

Use these as quick checks, not full category modules:

- 00: Block Green when scope, authorization, evidence safety, redaction, owner, or current-source basis is unclear.
- 01: Block Green when auth/session/MFA/recovery/token lifecycle, invalidation, identity ownership, or service-account scope is unclear.
- 02: Block Green unless trusted server-side or policy-layer authorization enforces the boundary.
- 03: Block Green unless data category, origin, audience, purpose, minimization, approval, retention, and sharing path are confirmed.
- 04: Block Green unless no raw secret is requested, pasted, logged, exposed, or used for unsafe validation, and scope/lifecycle/owner are confirmed.
- 05: Block Green unless untrusted input is constrained, parameterized, allowlisted, encoded where needed, and prevented from controlling dangerous execution or destinations.
- 06: Block Green unless authn/authz, scopes, data/actions, schemas, webhook trust, limits, logging, owner, and revocation are confirmed.
- 07: Block Green unless the browser is treated as untrusted, backend enforcement is confirmed, and sensitive browser data is minimized.
- 08: Block Green unless file sensitivity, audience, access policy, link expiry/revocation, processing isolation, cache behavior, and retention are confirmed.
- 09: Block Green unless workflow states, approvals, idempotency, quotas, caps, monitoring, owner, and abuse controls are confirmed.
- 10: Block Green unless exposure, environment, data sensitivity, effective permissions, lifecycle, and environment separation are confirmed.
- 11: Block Green unless dependency source/version/reachability, advisory status where material, CI/CD permissions, secrets, artifacts, registry controls, and owner review are confirmed.
- 12: Block Green unless transport path, certificate validation, approved algorithms/libraries, password hashing, key lifecycle, and fail-closed verification are confirmed.
- 13: Block Green unless runtime path, privilege, isolation, parser controls, diagnostics, worker trust, resource limits, dependency status, and script/tool ownership are confirmed.
- 14: Block Green unless safe log fields, event coverage, redaction, access controls, retention, alert routing, integrity, runbooks, and attribution are confirmed.
- 15: Block Green unless data category, approved tool/settings, connector scopes/actions, RAG/source authorization, retention, human approval gates, review, auditability, and revocation are confirmed.

## Quick Remediation Direction

Use short defensive guidance:

- Restrict access, remove exposure, and document owner approval.
- Rotate or revoke credentials where exposure is plausible.
- Replace raw evidence with synthetic, redacted, or local-only examples.
- Move secrets server-side and use managed secret storage.
- Enforce trusted server-side authorization and least privilege.
- Minimize sensitive data, logs, browser exposure, and vendor/AI sharing.
- Add approval gates, caps, quotas, retention, revocation, audit logs, and monitoring.
- Use current official docs or owner-confirmed settings when external facts affect the decision.

## Quick Escalation Triggers

Escalate or switch to Medium/Indepth when:

- Any Red condition is present.
- Orange or sensitive Gray remains unresolved.
- The action involves production systems, secrets, PII, customer data, auth/authz, broad permissions, cloud/IAM, CI/CD, AI agents, vendor exposure, external sharing, legal/privacy-sensitive unknowns, or high-impact automation.
- The user needs detailed code/config review, category-specific criteria, final approval, or a release gate decision.
