# 14. Logging, Monitoring, Auditability, and Incident Readiness

Category ID: 14

Category name: Logging, Monitoring, Auditability, and Incident Readiness

## Purpose

Review whether the right people can detect, understand, attribute, preserve safe evidence, and respond to suspicious, abusive, unauthorized, privacy-impacting, or operationally unsafe events without exposing secrets or private data.

## Core Review Question

Can the right people detect, understand, attribute, preserve safe evidence, and respond to suspicious, abusive, unauthorized, privacy-impacting, or operationally unsafe events without exposing secrets or private data?

## Scope

Application/API/auth/admin/identity/cloud/IAM/database/storage/CI/CD/SaaS/vendor/support/no-code/AI/automation/webhook/service logs, dashboards, SIEM/SOC alerts, runbooks, incident records, retention/access/log integrity/redaction/masking, and audit coverage for high-risk actions.

## Review Signals

- Logs, dashboards, traces, screenshots, incident records, prompts, tool logs, crash reports, or alerts may contain secrets or sensitive data.
- Sensitive or privileged actions may be unauditable.
- Logs can be altered, deleted, disabled, or ignored by the actor being audited.
- Alert routing, ownership, triage, retention, access, integrity, or runbooks are unclear.
- Vendor, cloud, SaaS, AI, no-code, or automation logging may be missing or unsafe.

## Red Conditions

- Live secret/credential in logs or incident evidence.
- Raw sensitive personal/customer/employee/production data exposed through logs.
- Public/broad sensitive logs, dashboards, traces, or incident evidence.
- Sensitive/privileged production actions unauditable.
- Audit logs alterable, deletable, or disableable by audited actors.
- Shared/generic privileged account makes high-risk actions unattributable.
- High-risk alerts intentionally disabled, ignored, or ownerless.
- Unsafe non-dev action creates serious audit/evidence exposure failure.

## Orange Conditions

- Sensitive action logging may be missing.
- Logs may contain secrets or credentials but type/exposure unclear.
- Logs may contain PII/private records but sensitivity/approval unclear.
- Alert owner, routing, triage, or response unclear.
- Cloud/identity/SaaS/vendor audit coverage unconfirmed.
- Retention, access, redaction, or provider behavior uncertain.
- AI/automation action logging or prompt/tool-log handling unclear.
- External log sharing lacks approval, redaction, or retention confirmation.

## Yellow Conditions

- Low-risk logging coverage gap.
- Documentation missing for functioning controls.
- Alert tuning issue for lower-risk owner-monitored events.
- Non-sensitive debug logging cleanup or time limit.
- Event schema improvement.
- Retention rationale or review cadence.
- Runbook or escalation refinement.

## Green Conditions

- Security events logged with safe metadata and no sensitive payloads.
- Privacy-preserving minimal logging supports investigations.
- Managed provider logging coverage, retention, and export verified.
- Actionable owner-routed alerts with runbooks.
- Log access, retention, and integrity controls protect evidence.
- Privileged/vendor/support actions attributable to named actors.
- AI/automation tool-call logs capture safe metadata, approvals, and outcomes.

## Gray Conditions

- Audit coverage, log contents, credential-like value, alert ownership, retention, provider behavior, shared/automation attribution, or incident readiness unknown.

## Required Evidence

- Event coverage.
- Safe fields logged.
- Redaction/masking.
- Access controls.
- Retention.
- Alert owner/routing.
- Integrity controls.
- Runbooks.
- Provider/vendor current docs.
- Attribution for privileged/AI/automation actions.

## Owners

Security owner, operations owner, developer, privacy owner, data owner, cloud/platform owner, identity owner, vendor owner, DevOps/release owner, and AI governance owner.

## Non-Dev Action Checks

Do not send raw logs, dashboards, alerts, traces, screenshots, crash reports, or incident notes to broad channels, vendors, or AI tools unless redacted and approved. Do not disable logs or alerts without owner approval.

## Unsafe Request Boundaries

Do not request raw logs with secrets/PII, private dashboards, incident evidence with sensitive data, tool-call payloads, or live credential validation. Use redacted event summaries and owner-confirmed settings.

## Safe Evidence Handling

Use safe metadata, redacted event examples, retention/access summaries, alert routing summaries, runbook summaries, and provider documentation. Do not include raw secrets, PII, private URLs, or sensitive screenshots.

## False-Positive Guardrails

Do not mark Green because logs are "internal", "encrypted", "vendor-managed", or "only admins can see them" without confirming access, retention, redaction, integrity, and owner routing.

## Under-Classification Guardrails

Treat secrets in logs, broad dashboards, disabled alerts, shared privileged accounts, unauditable actions, AI/tool logs, and incident exports as Orange or Red until safe controls are confirmed.

## Currentness Notes

Check current provider/vendor logging behavior, retention settings, export controls, AI/tool logging behavior, and security monitoring guidance when material.

## Category Gate Rule

Fails on secrets/PII in logs, broad sensitive dashboard exposure, unauditable high-risk actions, log tampering risk, disabled high-risk alerts, or unresolved auditability unknowns for sensitive areas.
