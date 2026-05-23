# Indepth Category Router

Use this router to choose primary and secondary categories. Load category files one by one as needed.

## Category Files

| ID | Category | File |
|---|---|---|
| 00 | Review Governance, Scope, and Evidence Handling | `category_00_review_governance.md` |
| 01 | Identity, Authentication, and Session Trust | `category_01_identity_auth_session.md` |
| 02 | Authorization, Access Control, and Trust Boundaries | `category_02_authorization_access_control.md` |
| 03 | Sensitive Data, PII, and Privacy Boundaries | `category_03_sensitive_data_privacy.md` |
| 04 | Secrets, Credentials, and Key Management | `category_04_secrets_credentials.md` |
| 05 | Input, Query, and Execution Safety | `category_05_input_query_execution.md` |
| 06 | API, Service, and Integration Boundaries | `category_06_api_service_integration.md` |
| 07 | Client-Side, Browser, and Frontend Exposure | `category_07_client_side_frontend.md` |
| 08 | File, Object, Content, and Storage Handling | `category_08_file_object_storage.md` |
| 09 | Business Logic, Abuse Prevention, and Resource Controls | `category_09_business_logic_abuse.md` |
| 10 | Configuration, Platform, Cloud, and Deployment Exposure | `category_10_platform_cloud_deployment.md` |
| 11 | Dependencies, Build, CI/CD, and Supply Chain Integrity | `category_11_supply_chain.md` |
| 12 | Cryptography, Transport, and Data Protection Controls | `category_12_crypto_transport.md` |
| 13 | Runtime, Memory, and Program Safety | `category_13_runtime_program_safety.md` |
| 14 | Logging, Monitoring, Auditability, and Incident Readiness | `category_14_logging_monitoring.md` |
| 15 | AI, Automation, and Agentic-System Safety | `category_15_ai_automation.md` |

## Routing Principles

- Use primary category ownership for the main failure mode.
- Add secondary categories when they improve owner routing, risk explanation, remediation, or gate impact.
- Prefer the cause category when the unsafe condition is caused by configuration, workflow, access, or architecture.
- Prefer the exposed-asset category when the user's question is about what leaked, what was mishandled, or who can see it.
- Use category 00 when evidence handling, scope, authorization, current-source basis, unsafe request handling, or escalation posture is itself the issue.
- Load all 16 category files only for explicit full gate or comprehensive all-surface review.

## Cross-Category Routing

| Case | Primary category | Secondary categories | Likely color when risky | Required owner | Required action | Safer alternative |
|---|---|---|---|---|---|---|
| Secret in frontend code | 04 Secrets | 07 Frontend | Red if secret/privileged; Orange if type/restrictions unknown | Security, developer, vendor/platform | Remove, rotate/revoke if plausible, move server-side or use documented publishable restricted key | Backend endpoint or publishable restricted key |
| PII in logs | 03 Sensitive Data | 14 Logging | Red if raw sensitive production data exposed; Orange if sensitivity/retention unknown | Privacy, data, security, developer | Remove/minimize, restrict access, fix filters, approve retention | Log metadata only |
| Public bucket with customer data | 08 Files/Storage or 10 Cloud Config | 03 Sensitive Data, 02 Authorization | Red if confirmed sensitive public access; Orange if contents unknown | Cloud/platform, security, data, privacy | Restrict, revoke links, review access, document remediation | Named least-privilege access |
| AI tool with CRM access | 15 AI/Automation | 02 Authorization, 06 API, 03 Sensitive Data | Red if broad write/export without approval; Orange if scopes unknown | AI governance, vendor, security, data, identity | Scope connector, approve data use, add logs, human approval, revocation | Approved least-privilege read-only connector |
| API returns excessive sensitive data | 06 API | 03 Sensitive Data, 02 Authorization | Red if unauthorized/cross-boundary; Orange if necessity/audience unknown | Developer, data, privacy, security | Response shaping, authorization, minimization | Return only necessary fields |
| Shared admin accounts | 01 Identity | 02 Authorization, 14 Auditability | Red for high-risk shared privileged access; Orange if scope unclear | Identity, security, operations | Replace with named accounts, MFA, least privilege, audit logs | Named time-bound access |
| Source maps exposing secrets | 11 Supply Chain or 07 Frontend | 04 Secrets, 10 Cloud Config | Red if real secret/sensitive production artifact; Orange if contents unknown | DevOps/release, developer, security | Remove artifact, rotate/revoke if needed, adjust build controls | Restricted source maps or no production maps |
| Vendor integration with broad API access | 06 API/Integration | 02 Authorization, 04 Secrets, 15 AI/Automation if AI/no-code | Orange until scopes/data/retention approved; Red if unapproved sensitive access confirmed | Vendor, security, data, identity | Least privilege, approval, audit, retention, revocation | Approved scoped integration |
| Production data in staging/demo | 03 Sensitive Data or 10 Cloud Config | 02 Authorization, 08 Files | Red if uncontrolled; Orange if data origin unknown | Developer, DevOps, data, privacy, security | Replace with synthetic/masked data, restrict access, approve exceptions | Synthetic or approved masked fixture |
| No-code automation using personal admin credentials | 15 AI/Automation | 01 Identity, 04 Secrets, 06 API | Red for production/high-impact access; Orange if scope unknown | AI governance, identity, security, vendor | Use scoped service identity, secure storage, logs, revocation | Managed service connector |
| AI-generated code used in production | 15 AI/Automation or 11 Supply Chain | 05 Input/Execution, 13 Runtime | Red if unreviewed high-impact; Orange if review status unknown | Developer, security, DevOps, AI governance | Code review, safe testing, change control | Advisory use plus normal review |
| Public dashboard with customer data | 03 Sensitive Data or 14 Logging | 02 Authorization, 10 Cloud Config | Red if confirmed public/broad sensitive data; Orange if data/audience unknown | Data, privacy, security, product, cloud/platform | Restrict, minimize, audit, owner approve | Role-limited dashboard |
| Debug mode enabled in production | 10 Cloud Config | 14 Logging, 03/04 if data/secrets exposed | Red if public production and sensitive output; Orange if environment/sensitivity unknown | Developer, DevOps, security, platform | Disable/restrict diagnostics, sanitize output | Restricted diagnostics channel |
| Dependency vulnerability in reachable production code | 11 Supply Chain | 13 Runtime if native/parser, 10 Cloud if deployment relevant | Red for reachable known exploited/high-impact without mitigation; Orange if reachability unknown | Developer, security, DevOps | Patch/mitigate/isolate or documented time-bound acceptance | Pinned patched dependency |

## Action Safety Routing

For non-dev safety questions:

1. State the direct answer.
2. Assign decision color, severity, confidence, and gate result.
3. Explain the practical concern briefly.
4. Ask only safe context if needed.
5. Name the owner to consult.
6. Give a safer alternative.
7. Remind the user not to provide raw secrets, PII, private screenshots, private links, or unsafe validation output.

Common action routing:

| Proposed action | Primary category | Likely risky color | Safe context to ask for | Safer alternative |
|---|---|---|---|---|
| API key in frontend/landing page | 04, 07 | Red if secret/privileged; Orange if unknown | Vendor docs, restrictions, scopes, owner | Backend endpoint or publishable restricted key |
| Customer data export | 03 | Red if unapproved; Orange if approval/retention unknown | Data class, purpose, audience, retention, approval | Redacted/minimized export or approved system |
| Production data in AI tools | 15, 03 | Red if unapproved real sensitive data; Orange if settings unknown | Approved tool, workspace settings, data category | Synthetic/redacted data in approved enterprise tool |
| Public bucket/resource | 08, 10 | Red if sensitive confirmed; Orange if contents unknown | Resource type, intended audience, data class, approval | Named least-privilege access |
| Screenshots with PII | 03, 00 | Red if raw sensitive data shared; Yellow if redaction cleanup | Whether fully redacted and audience approved | Redacted screenshot or text summary |
| Third-party automation | 15, 06 | Red for high-impact unapproved actions; Orange if scopes unknown | Scopes, read/write actions, logs, owner, retention | Scoped approved connector with human approval |
| Production credentials in tests | 04, 11 | Red | Whether isolated test credentials can be used | Test credentials, synthetic data, secret manager |
| Vendor access | 01, 02, 06 | Orange by default; Red if shared admin/high-impact uncontrolled | Named account, MFA, scope, duration, audit, approval | Named least-privilege time-bound access |
| Broad cloud permissions | 10, 02 | Red if unapproved production control; Orange if scope unknown | Role scope, duration, approval, audit | Least-privilege time-bound role |
| AI agent connected to company systems | 15, 02, 06 | Red for ungated high-impact actions; Orange if scopes unknown | Tools, scopes, actions, approval gates, logs, owner | Read-only scoped tool with human approval |
