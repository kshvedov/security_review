# Medium Review

Medium mode is the default normal review depth. It supports practical security reviews without loading all Indepth category files.

Use this file with the shared references:

- `../shared/output_format.md`
- `../shared/universal_safety_rules.md`
- `../shared/classification_model.md`
- `../shared/current_source_policy.md`
- `../shared/redaction_and_unsafe_requests.md`
- `../shared/pass_fail_logic.md`
- `../shared/style_policy.md`

Do not redefine the shared output format here. Use `../shared/output_format.md` for every Medium result.

## When To Use Medium

Use Medium by default for normal security reviews involving code, configuration, APIs, cloud, auth, authorization, data, AI, vendor tools, files, logs, permissions, integrations, dependencies, runtime behavior, or moderate risk.

Stay in Medium when the user needs practical category guidance but has not asked for final-gate or comprehensive review depth.

Switch to Indepth when the user asks for deep, comprehensive, full, final-gate, or release-blocking review, or when the request involves high-risk production impact, secrets, PII, auth/authz, cloud/IAM, CI/CD, AI agents, vendor exposure, broad permissions, customer data, or legal/privacy-sensitive unknowns.

Do not infer whether the user is technical or non-technical. Use the requested style. If no style is specified, use clear, plain, precise language.

## Required Medium Reading Flow

1. Read the shared references needed for the review.
2. Read `category_router.md`.
3. Select the likely primary category and useful secondary categories.
4. Load only the relevant Medium category group files:
   - `categories_00_03.md`
   - `categories_04_07.md`
   - `categories_08_11.md`
   - `categories_12_15.md`
5. Use `../shared/output_format.md` for the final review result.

Do not load all category groups unless the request is broad enough to need them.

## Medium Output Density

Medium output covers major issue families with practical remediation and owner routing.

- Name each major risk family that changes owner routing, gate result, or remediation.
- Group related instances instead of listing every duplicate line or occurrence.
- Include representative evidence for each major family.
- Do not compress distinct families into one vague finding when they have different fixes or owners.
- When both are present, keep browser-visible credential-like material separate from browser-visible sensitive business metadata.

For technical reviews, keep distinct families separate when present, including secrets, sensitive data, browser or frontend exposure, browser-delivered hidden state, authorization boundaries, file/export exposure, privileged actions, platform/configuration, logging/auditability, and unsafe rendering.

## Review Modes

Use Technical Review Mode for code, configuration, API behavior, queries, logs, files, browser/frontend evidence, cloud settings, CI/CD settings, dependency evidence, identity/session settings, authorization logic, runtime behavior, AI/automation configuration, or vendor integrations.

Safe Technical Review inputs include redacted code/config snippets, architecture descriptions, redacted settings summaries, redacted API/request/response summaries, synthetic examples, local fixtures, safe scan summaries, official documentation, owner confirmations, and current-source lookup results.

Use Action Safety Mode when a user asks whether a proposed action is safe, acceptable, risky, or allowed. Answer directly, classify the action, ask only for safe context, name owner escalation where required, and provide a safer alternative.

## Medium Review Workflow

1. Identify the review mode.
2. Confirm scope and safe evidence handling.
3. Select primary and secondary categories using `category_router.md`.
4. Load only the relevant category group file or files.
5. Apply shared Red, Orange, Yellow, Green, and Gray rules.
6. Keep severity, confidence, and gate result separate.
7. Apply current-source verification from `../shared/current_source_policy.md` when currentness materially affects the decision.
8. Apply shared redaction and unsafe request handling.
9. Apply shared pass/fail logic.
10. Use the shared output format.

## Action Safety Behavior

For proposed actions, give a direct answer:

- "Do not proceed as described" for Red or clearly unsafe actions.
- "Proceed only if these conditions are confirmed" for Orange, Gray, or context-dependent actions.
- "This looks acceptable based on the provided safe context" only when Green is supported by safe evidence and current-source checks where material.
- Use `../shared/pass_fail_logic.md` to decide whether ticketing or documented acceptance is allowed.

Ask only for safe context:

- Data category and whether it is synthetic, redacted, public, or production-derived.
- Owner, approval status, intended audience, and retention.
- Access scope, read/write capability, MFA, named accounts, logging, and revocation.
- Current official documentation or owner-confirmed settings when external facts affect classification.

Never ask for raw keys, tokens, passwords, PII, private screenshots, live links, production records, unsafe validation output, exploit proof, or credential testing.

## Medium Escalation Triggers

Escalate or switch to Indepth when:

- Any Red condition is present.
- Orange or sensitive Gray remains unresolved.
- The request involves production systems, secrets, PII, customer data, auth/authz, broad permissions, cloud/IAM, CI/CD, AI agents, vendor exposure, external sharing, legal/privacy-sensitive unknowns, or high-impact automation.
- The user needs final approval, a release gate decision, comprehensive category coverage, or deep source-specific analysis.

## Medium Consistency Check

Before finalizing:

- All selected categories are identified by ID and name.
- Major issue families that affect owners, remediation, or gate result are not collapsed into one broad finding.
- Shared classification, current-source, redaction, pass/fail, and style policies were applied from the shared files.
- Evidence, assumptions, unknowns, required confirmation, redactions, safer alternatives, and gate impact are separated.
- Missing critical context is not treated as safe.
