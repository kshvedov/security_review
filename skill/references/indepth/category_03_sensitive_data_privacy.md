# 03. Sensitive Data, PII, and Privacy Boundaries

Category ID: 03

Category name: Sensitive Data, PII, and Privacy Boundaries

## Purpose

Review whether sensitive, personal, customer, employee, production, and confidential business data is collected, processed, stored, displayed, logged, exported, retained, deleted, shared, and used with appropriate boundaries.

## Core Review Question

Is sensitive data handled only where necessary, only by appropriate parties, with safe redaction, minimization, storage, sharing, retention, deletion, and review boundaries?

## Scope

Sensitive data collection, processing, storage, transmission, display, logging, export, retention, deletion, sharing, AI/vendor/tool use, customer records, employee data, private messages, support tickets, screenshots, dashboards, reports, production exports, prompts, and generated artifacts.

## Review Signals

- Real or production-like customer, employee, private, financial, health, legal, support, CRM, usage, or confidential business data appears in evidence.
- Sensitive data is sent to vendors, AI tools, support portals, dashboards, logs, analytics, session replay, files, exports, or lower-trust environments.
- Data is described as anonymized, masked, test, demo, internal, or aggregated without evidence.
- Retention, deletion, ownership, approval, and audience are unclear.

## Red Conditions

- Real sensitive data exposed outside approved scope.
- Public or link-accessible sensitive artifact.
- Cross-actor sensitive API/page exposure.
- Unapproved vendor/AI/automation processing.
- Production sensitive data in uncontrolled non-production workflow.
- Sensitive data leakage through logs, observability, or browser-visible surfaces.
- Tracking/session replay captures sensitive data.
- Raw sensitive evidence reproduced in review material.
- Unsafe retention after deletion or purpose end.

## Orange Conditions

- Likely sensitive exposure with missing origin/audience.
- Public/shared artifact with unknown sensitive content.
- External/tool processing controls unknown.
- Production-like data in lower-control workflow.
- Linkable dataset or identifier logging unresolved.
- Tracking on sensitive surface with unknown collection.
- Retention/deletion coverage or broad internal access unclear.
- Auditability for sensitive-data actions unresolved.

## Yellow Conditions

- Unnecessary identifiers in controlled internal logs.
- Non-sensitive over-return to authorized audience.
- Bounded retention documentation gap.
- Approved tool workflow needs minimization documentation.
- Controlled export lacks expiry or review cadence.
- Sensitive-looking metadata with limited visibility.
- Minor redaction improvement.

## Green Conditions

- Confirmed synthetic or approved demo data.
- Properly redacted evidence.
- Expected current-user self-service data.
- Approved role-limited internal access.
- Safe aggregate analytics.
- Approved third-party/AI/tool processing.
- Non-sensitive browser state.
- Expected public business information.

## Gray Conditions

- Data origin/sensitivity, realistic test-data origin, anonymization/de-identification claim, retention/deletion/tool/vendor/shared-link risk, or broad internal need-to-know controls unknown.

## Required Evidence

- Data category and origin.
- Intended audience and purpose.
- Approval status.
- Minimization.
- Retention and deletion.
- Sharing path.
- Vendor/AI settings.
- Current-source data/tool handling basis where material.

## Owners

Privacy owner, data owner, security owner, developer, product owner, vendor owner, legal/compliance owner, AI governance owner, and operations owner.

## Non-Dev Action Checks

Do not upload or share raw customer/employee records, screenshots, support tickets, logs, exports, prompts, or private links. Use synthetic/redacted data and approved tools with confirmed retention/access controls.

## Unsafe Request Boundaries

Do not request or reproduce raw PII, customer records, employee records, private messages, support tickets, production exports, raw screenshots, or sensitive prompts. Ask for data category, location, exposure surface, audience, owner, and required action.

## Safe Evidence Handling

Use redacted summaries, synthetic examples, local-only fixtures, architecture descriptions, safe configuration summaries, permission summaries, owner confirmations, and current official documentation when provider behavior matters.

## False-Positive Guardrails

Do not mark Green because data is "internal", "test", "masked", "anonymized", "encrypted", or "only in logs". Require data-owner evidence and access/retention controls.

## Under-Classification Guardrails

Treat small populations, stable identifiers, precise times/locations, support tickets, dashboards, logs, screenshots, and production-like data as potentially sensitive until proven otherwise.

## Currentness Notes

Check current vendor/AI retention, data-use, privacy, deletion, analytics, session replay, and platform behavior when external handling or Green depends on those facts.

## Category Gate Rule

Fails on confirmed sensitive-data exposure, unapproved external/tool processing, unsafe public sharing, raw sensitive evidence, uncontrolled production-data use, or unresolved sensitive-data unknowns.
