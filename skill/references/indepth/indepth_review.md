# Indepth Review

Indepth mode is for comprehensive reviews, final gate reviews, high-risk decisions, and requests that need category-by-category reasoning.

Use this file with the shared references:

- `../shared/output_format.md`
- `../shared/universal_safety_rules.md`
- `../shared/classification_model.md`
- `../shared/current_source_policy.md`
- `../shared/redaction_and_unsafe_requests.md`
- `../shared/pass_fail_logic.md`
- `../shared/style_policy.md`

Do not redefine the shared output format here. Use `../shared/output_format.md` for every Indepth result.

## When To Use Indepth

Use Indepth when:

- The user asks for deep, comprehensive, full, final-gate, release-blocking, or all-surface review.
- The request involves high-risk production impact, secrets, PII, auth/authz, cloud/IAM, CI/CD, AI agents, vendor exposure, broad permissions, customer data, external sharing, or legal/privacy-sensitive unknowns.
- The request needs category-by-category reasoning, owner routing, gate impact, and safe remediation across multiple surfaces.

Do not infer whether the user is technical or non-technical. Use the requested style. If no style is specified, use clear, plain, precise language.

## Required Indepth Reading Flow

1. Read the shared references needed for the review.
2. Read `category_router.md`.
3. Select primary and useful secondary categories.
4. Load category files one by one as needed.
5. Load all 16 category files only when the user explicitly asks for a full gate, comprehensive all-surface review, or category-by-category review and context allows that depth.
6. Use `../shared/output_format.md` for the final review result.

## Indepth Output Density

Indepth output is comprehensive issue-family coverage for the supplied context. It is not a duplicate finding register unless the user asks for a full inventory.

- Explicitly cover every material distinct risk family observed in the supplied evidence.
- Group duplicate instances under the same family.
- Include representative evidence for each family.
- Keep findings grouped by color in the shared output format.
- Do not omit a material family because another higher-risk family already causes Fail.

For technical reviews, cover relevant families such as credential exposure, sensitive embedded or downloadable data, client-side auth/admin logic, browser storage, unsafe rendering, global/bootstrap exposure, HTTP or internal routes, operational comments, missing CSP or equivalent browser hardening when visible, privileged actions, file/export exposure, platform/configuration, logging/auditability, identity/session handling, and backend enforcement gaps.

## Review Modes

Use Technical Review Mode for code, configuration, API behavior, queries, logs, files, browser/frontend evidence, cloud settings, CI/CD settings, dependency evidence, identity/session settings, authorization logic, runtime behavior, AI/automation configuration, or vendor integrations.

Use Action Safety Mode when a user asks whether a proposed action is safe, acceptable, risky, or allowed. Give a direct answer first, classify the action, ask only for safe context, name the owner when escalation is needed, and provide a safer alternative.

## Indepth Workflow

1. Define the review boundary and mode.
2. Redact or refuse unsafe evidence before classification.
3. Identify primary and secondary categories.
4. Load relevant category files.
5. Apply category Red/Orange/Yellow/Green/Gray triggers.
6. Separate severity, confidence, and gate result.
7. Record current-source verification where currentness is material.
8. Identify owners and required confirmation.
9. Provide safe remediation and safer alternatives.
10. Apply shared pass/fail logic.
11. Use the shared output format.

## Currentness

Use `../shared/current_source_policy.md` as the authority. Category files add category-specific currentness notes only.

## Final Gate Behavior

For final gate review, use `../shared/pass_fail_logic.md` as the authority for Pass, Fail, Needs escalation, Needs more context, Can pass with ticketing, and Can pass with documented acceptance. Indepth category files provide the category-specific evidence and owner routing needed to apply that gate logic.

## Report Safety

Use `../shared/redaction_and_unsafe_requests.md` and `../shared/style_policy.md` as the authorities for report safety, unsafe request handling, redaction, tone, and legal/privacy/compliance escalation boundaries.

## Indepth Consistency Check

Before finalizing:

- Technical Review Mode or Action Safety Mode is clear.
- Primary and secondary categories are named by ID and title.
- All material distinct issue families in the supplied context are covered with representative evidence.
- Duplicate instances are grouped unless the user asks for a full issue inventory.
- Shared classification, current-source, redaction, pass/fail, and style policies were applied from the shared files.
- Evidence, assumptions, unknowns, required confirmation, redactions, safer alternatives, and gate impact are separated.
- Owner escalation and safe remediation are included.
- Missing critical context and absent public vulnerability evidence are not treated as safe.
