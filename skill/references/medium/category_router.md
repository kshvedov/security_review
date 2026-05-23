# Medium Category Router

Use this router to choose the primary category and useful secondary categories. Load only the category group files needed for the review.

## Category Groups

| IDs | File | Use for |
|---|---|---|
| 00-03 | `categories_00_03.md` | Review governance, identity, authorization, sensitive data, PII, and privacy boundaries. |
| 04-07 | `categories_04_07.md` | Secrets, input/query/execution safety, APIs/services/integrations, frontend/browser exposure. |
| 08-11 | `categories_08_11.md` | Files/storage, business logic/abuse controls, cloud/platform/deployment, dependencies/build/CI/CD/supply chain. |
| 12-15 | `categories_12_15.md` | Crypto/transport/data protection, runtime/program safety, logging/monitoring/auditability, AI/automation/agents. |

## Category Index

| ID | Category |
|---|---|
| 00 | Review Governance, Scope, and Evidence Handling |
| 01 | Identity, Authentication, and Session Trust |
| 02 | Authorization, Access Control, and Trust Boundaries |
| 03 | Sensitive Data, PII, and Privacy Boundaries |
| 04 | Secrets, Credentials, and Key Management |
| 05 | Input, Query, and Execution Safety |
| 06 | API, Service, and Integration Boundaries |
| 07 | Client-Side, Browser, and Frontend Exposure |
| 08 | File, Object, Content, and Storage Handling |
| 09 | Business Logic, Abuse Prevention, and Resource Controls |
| 10 | Configuration, Platform, Cloud, and Deployment Exposure |
| 11 | Dependencies, Build, CI/CD, and Supply Chain Integrity |
| 12 | Cryptography, Transport, and Data Protection Controls |
| 13 | Runtime, Memory, and Program Safety |
| 14 | Logging, Monitoring, Auditability, and Incident Readiness |
| 15 | AI, Automation, and Agentic-System Safety |

## Routing Principles

- Use the primary category for the main failure mode.
- Add secondary categories only when they improve the finding, owner routing, or remediation.
- Prefer the cause category when the unsafe condition comes from configuration or workflow design.
- Prefer the exposed-asset category when the user's question is about what leaked or what was mishandled.
- Use category 00 when scope, authorization, evidence safety, redaction, unsafe request handling, current-source basis, or escalation posture is itself the main issue.
- Use shared output, classification, pass/fail, redaction, current-source, and style rules for every category.

## Cross-Category Routing

| Case | Primary | Secondary | Likely risky color | Required action |
|---|---|---|---|---|
| Secret in frontend code | 04 | 07 | Red if secret/privileged; Orange if type or restrictions unknown. | Remove, rotate or revoke if plausible, move server-side or use documented publishable restricted key. |
| PII in logs | 03 | 14 | Red if raw sensitive production data exposed; Orange if sensitivity or retention unknown. | Remove or minimize, restrict access, fix filters, approve retention. |
| Public bucket with customer data | 08 or 10 by cause | 03, 02 | Red if confirmed sensitive public access; Orange if contents unknown. | Restrict, revoke links, review access, document remediation. |
| AI tool with CRM/API access | 15 | 02, 03, 06, 04 | Red if broad write/export without approval; Orange if scopes unknown. | Scope connector, approve data use, add logs, human approval, revocation. |
| API returns excessive sensitive data | 06 | 03, 02 | Red if unauthorized or cross-boundary; Orange if necessity or audience unknown. | Response shaping, authorization, minimization. |
| Shared admin accounts | 01 | 02, 14 | Red for high-risk shared privileged access; Orange if scope unclear. | Replace with named accounts, MFA, least privilege, audit logs. |
| Source maps exposing secrets | 11 or 07 by artifact path | 04, 10 | Red if real secret or sensitive production artifact; Orange if contents unknown. | Remove artifact, rotate or revoke if needed, adjust build controls. |
| Vendor integration with broad API access | 06 | 02, 04, 15 if AI/no-code | Orange until scopes/data/retention are approved; Red if unapproved sensitive access is confirmed. | Least privilege, approval, audit, retention, revocation. |
| Production data in staging/demo | 03 or 10 by cause | 02, 08 | Red if uncontrolled; Orange if data origin unknown. | Replace with synthetic or masked data, restrict access, approve exceptions. |
| No-code automation using personal admin credentials | 15 | 01, 04, 06 | Red for production or high-impact access; Orange if scope unknown. | Use scoped service identity, secure storage, logs, revocation. |
| AI-generated code used in production | 15 or 11 | 05, 13 | Red if unreviewed high-impact; Orange if review status unknown. | Code review, safe testing, change control. |
| Public dashboard with customer data | 03 or 14 | 02, 10 | Red if public or broadly shared sensitive data; Orange if data/audience unknown. | Restrict, minimize, audit, owner approve. |
| Debug mode enabled in production | 10 | 14, 03, 04 | Red if public production and sensitive output; Orange if environment or sensitivity unknown. | Disable or restrict diagnostics, sanitize output. |
| Dependency vulnerability in reachable production code | 11 | 13, 10 | Red for reachable known exploited/high-impact without mitigation; Orange if reachability/current status unknown. | Patch, mitigate, isolate, or document time-bound acceptance. |

## Action Safety Routing

| Proposed action | Default concern | Likely risky color | Safe context to ask for | Never request | Safer alternative |
|---|---|---|---|---|---|
| Put API key in frontend | Secret may become public. | Red if secret/privileged; Orange if unknown. | Vendor docs, restrictions, scopes, owner. | Raw key. | Backend endpoint or publishable restricted key. |
| Export customer data | Sensitive data may leave controls. | Red if unapproved; Orange if approval/retention unknown. | Data class, purpose, audience, retention, approval. | Raw rows/CSV. | Redacted or minimized approved export. |
| Use production data in AI | External retention/model/logging risk. | Red if unapproved sensitive data; Orange if settings unknown. | Approved tool, workspace settings, data category. | Raw prompt, files, or records. | Synthetic or redacted data in approved enterprise tool. |
| Make bucket/resource public | Private data or control may become public. | Red if sensitive confirmed; Orange if contents unknown. | Resource type, audience, data class, approval. | Live URLs or object names. | Named least-privilege access. |
| Send screenshots/logs to vendor | Evidence may contain secrets/PII. | Red if raw sensitive data; Orange if contents unknown. | Data categories, redaction, vendor approval, retention. | Raw screenshot or log. | Redacted summary. |
| Connect third-party automation | May read/write/export/delete at scale. | Red for high-impact unapproved actions; Orange if scopes unknown. | Scopes, read/write actions, logs, owner, retention. | Tokens or private records. | Scoped approved connector with human approval. |
| Use production credentials in tests | Credentials may leak or affect production. | Red. | Whether isolated test credentials exist. | Credential value. | Test credentials, synthetic data, secret manager. |
| Grant vendor/shared admin access | Accountability and revocation may fail. | Red for high-risk; Orange if scope unknown. | Named account, MFA, scope, duration, audit, approval. | Passwords or tokens. | Named least-privilege time-bound access. |
| Disable MFA or protections | Account takeover/control loss risk. | Red for privileged/sensitive access. | Time-bound emergency exception and owner approval. | MFA or recovery codes. | Conditional exception with approval and expiry. |
| Broad cloud permissions | Large blast radius. | Red if unapproved production control; Orange if scope unknown. | Role scope, duration, approval, audit. | Account IDs or secrets. | Least-privilege time-bound role. |
| AI agent connected to company systems | Passive access can become active impact. | Red for ungated high-impact actions; Orange if scopes unknown. | Tools, scopes, actions, approval gates, logs, owner. | Tokens or prompts with records. | Read-only scoped tool with human approval. |
| Public form triggering backend actions | Spam/cost/data processing risk. | Red for uncontrolled high-impact side effects; Orange if controls unknown. | Rate limits, validation, downstream actions, monitoring. | Live abuse outputs. | Validation, caps, queue, approval. |
