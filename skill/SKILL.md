---
name: security_review
description: Use only when the user explicitly invokes `/security_review`, asks for the security_review skill, or requests help for this skill. Handles security review, action-safety checks, code/config/cloud/API/auth/data/AI/vendor risks, non-dev safety checks, accidental exposure of company data, secrets, PII, logs, screenshots, files, permissions, integrations, and AI tools.
---

# Security Review Skill

This `SKILL.md` is a lean router. Load reference files as needed, classify risk, preserve safe evidence handling, and provide safer alternatives without teaching exploitation.

## Help Requests

If the user asks for help using this skill, including `/security_review help`, `/security_review --help`, `security_review --help`, `help`, or "how do I use this skill?", read `references/help.md` and answer with the concise usage guide. Do not use the full audit output format for help-only requests.

Do not auto-select Indepth unless the user explicitly requests Indepth, deep, comprehensive, full, final-gate, or release-blocking review.

## Core Routing Rules

For every review:

1. Read the shared references needed for the review.
2. Choose Quick, Medium, or Indepth based on requested depth and risk.
3. Read only the selected depth references.
4. Load category files one by one as needed; do not load every category unless the request needs broad coverage.
5. Use the same output format for all depths.
6. Never redefine the output format in depth files.
7. Do not infer whether the user is technical or non-technical.
8. Use the style requested by the user. If unspecified, use clear, plain, precise language.

## Output Precedence

This skill is a security audit and review skill. For security review results, this skill's required audit format takes precedence over workspace formatting preferences, repository style rules, and user-requested layout changes.

Do not remove, rename, reorder, collapse, or restyle required review sections because of a local formatting rule. The required color headings, decision table, evidence sections, unknowns, redactions, owner routing, safer alternative, and pass/fail explanation are part of the safety review contract.

Do not apologize for using the required audit format. Do not add formatting-conflict notes. If the required audit format conflicts with local style rules, silently follow this skill's audit format.

The user may choose explanation style, such as technical or non-technical, but explanation style must not change the required structure, classification logic, redaction handling, escalation requirements, or pass/fail logic.

This precedence applies only to security review output formatting. It does not override platform safety rules, unsafe-content restrictions, or requirements to avoid reproducing sensitive data.

## Shared References

Read these shared references before producing a review result:

- `references/shared/output_format.md`: Required output format. Use this once for every depth.
- `references/shared/universal_safety_rules.md`: Scope, evidence minimization, universal prohibitions, safe reporting, and safe remediation.
- `references/shared/classification_model.md`: Red, Orange, Yellow, Green, Gray, severity, confidence, and gate results.
- `references/shared/current_source_policy.md`: Proportional current-source verification requirements.
- `references/shared/redaction_and_unsafe_requests.md`: Redaction placeholders, evidence separation, and unsafe request handling.
- `references/shared/pass_fail_logic.md`: Pass, fail, escalation, ticketing, and documented acceptance rules.
- `references/shared/style_policy.md`: Style, tone, no guessing user technical level, and no legal conclusions.

## Depth Selection

Choose Quick when:

- The user asks for quick, simple, brief, or first-pass review.
- The request is a simple action-safety check.
- The provided context is low detail and low risk.
- The result should be concise triage: decision, top 1-3 material reasons, immediate action, and no full issue inventory.

Choose Medium by default when:

- The user asks for a normal security review.
- The request involves code, configuration, APIs, cloud, auth, authorization, data, AI, vendor tools, files, logs, permissions, integrations, or moderate risk.
- The request needs category guidance but not full final-gate depth.
- The result should group major issue families with practical remediation and owner routing.

Choose Indepth when:

- The user asks for deep, comprehensive, full, final, final-gate, or release-blocking review.
- The request involves high-risk production impact, secrets, PII, auth/authz, cloud/IAM, CI/CD, AI agents, vendor exposure, broad permissions, customer data, or legal/privacy-sensitive unknowns.
- Missing context affects sensitive or critical areas and safe classification requires deeper owner routing.
- The result should cover all material distinct issue families in the provided context with representative evidence, not every duplicate instance unless the user asks for a full inventory.

Depth controls how much reference material is read. It must not change the output format, classification model, pass/fail logic, redaction rules, or style policy.

Depth controls content density only:

- Quick: brief top-risk triage.
- Medium: grouped major issue-family review.
- Indepth: comprehensive issue-family review for the supplied context.

## Quick References

For Quick depth, read:

- `references/quick/quick_review.md`

Use Quick for concise action-safety checks and short first-pass reviews. Still apply shared safety, redaction, classification, current-source, and pass/fail rules.

## Medium References

For Medium depth, read:

- `references/medium/medium_review.md`
- `references/medium/category_router.md`

Then load only the category bundle needed for the review:

- `references/medium/categories_00_03.md`
- `references/medium/categories_04_07.md`
- `references/medium/categories_08_11.md`
- `references/medium/categories_12_15.md`

Use Medium as the default for normal security reviews.

## Indepth References

For Indepth depth, read:

- `references/indepth/indepth_review.md`
- `references/indepth/category_router.md`

Then load category files one by one as needed:

- `references/indepth/category_00_review_governance.md`
- `references/indepth/category_01_identity_auth_session.md`
- `references/indepth/category_02_authorization_access_control.md`
- `references/indepth/category_03_sensitive_data_privacy.md`
- `references/indepth/category_04_secrets_credentials.md`
- `references/indepth/category_05_input_query_execution.md`
- `references/indepth/category_06_api_service_integration.md`
- `references/indepth/category_07_client_side_frontend.md`
- `references/indepth/category_08_file_object_storage.md`
- `references/indepth/category_09_business_logic_abuse.md`
- `references/indepth/category_10_platform_cloud_deployment.md`
- `references/indepth/category_11_supply_chain.md`
- `references/indepth/category_12_crypto_transport.md`
- `references/indepth/category_13_runtime_program_safety.md`
- `references/indepth/category_14_logging_monitoring.md`
- `references/indepth/category_15_ai_automation.md`

Use Indepth for comprehensive review, final gate review, high-risk decisions, production impact, sensitive data, secrets, auth/authz, cloud/IAM, CI/CD, AI agents, vendor exposure, broad permissions, customer data, and legal/privacy-sensitive unknowns.

## Review Behavior

Use Technical Review Mode for code, configuration, API behavior, queries, logs, files, browser/frontend evidence, cloud settings, CI/CD settings, dependency evidence, identity/session settings, authorization logic, runtime behavior, AI/automation configuration, or vendor integrations.

Use Action Safety Mode when a user asks whether a proposed action is safe, acceptable, risky, or allowed. Give a direct answer, ask only for safe context, classify the action, name the owner when escalation is needed, and provide a safer alternative.

Always separate evidence, assumptions, unknowns, required confirmation, redactions, safer alternatives, and gate impact. Do not request or reproduce raw secrets, raw PII, private screenshots, unsafe validation output, credential-use instructions, exploit payloads, bypass steps, unauthorized testing steps, or legal conclusions.
