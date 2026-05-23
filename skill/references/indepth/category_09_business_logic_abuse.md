# 09. Business Logic, Abuse Prevention, and Resource Controls

Category ID: 09

Category name: Business Logic, Abuse Prevention, and Resource Controls

## Purpose

Review whether intended features, workflows, state transitions, approvals, billing-like flows, quotas, messaging triggers, public forms, bulk actions, automation, and overrides can be misused to bypass rules, abuse resources, create operational harm, or create business/security impact.

## Core Review Question

Can someone use allowed features in an unintended way to bypass rules, abuse resources, cause operational harm, or create business/security impact?

## Scope

Workflow integrity, state transitions, approvals, checkout, billing, refunds, credits, discounts, coupons, trials, referrals, entitlements, quotas, signup/invite/account-existence flows, public forms/links/webhooks, exports/search/sync/bulk actions/background jobs, messaging triggers, rate limits, cost controls, AI/no-code/vendor automation, and admin/support/finance/operations overrides.

## Review Signals

- A valid action can be repeated, retried, refreshed, automated, or triggered publicly.
- State, approval, quota, idempotency, or separation-of-duties controls are unclear.
- Client-controlled values influence authoritative outcomes.
- Bulk, messaging, export, costly, or high-impact actions lack caps, monitoring, or owner approval.
- Automation or no-code tooling amplifies action volume or permissions.

## Red Conditions

- Unbounded repeatable sensitive or costly workflow.
- Workflow order, approval, state, or separation-of-duties bypass with serious impact.
- Client-controlled business-critical value affects authoritative outcome.
- Public unauthenticated flow triggers high-impact, costly, external, or sensitive side effects without meaningful controls.
- Bulk export/search/report/sync exposes sensitive data without limits, approval, or audit.
- High-volume messaging/invite/notification/webhook trigger lacks caps, suppression, or monitoring.
- Expensive operation repeatable at high volume without controls.
- Admin/support override bypasses high-risk controls without approval, audit, or expiry.
- AI/automation amplifies high-impact actions without approval, limits, or logging.

## Orange Conditions

- Potentially repeatable/costly/sensitive flow with duplicate prevention, idempotency, quotas, monitoring, approval, or business owner unknown.
- Public forms, bulk exports, message triggers, AI/tool costs, or override paths have unclear controls.
- Rate limit boundary may not match the business entity at risk.

## Yellow Conditions

- Low-risk workflow/quota documentation gap.
- Minor alerting, monitoring, or rate-limit tuning issue.
- Controlled override/access path needs expiry or review cadence.
- Abuse scenario should be ticketed but is not a current blocker.

## Green Conditions

- Retries idempotent, bounded, monitored, and owner-approved.
- Workflow states and approvals enforced server-side with audit logs.
- Business-critical values recomputed or validated server-side.
- Public flows validated, rate-limited, monitored, low-impact, and approved.
- Bulk access role-limited, logged, capped, approved, and aligned to sensitivity.
- Automation least-privilege, capped, human-confirmed for sensitive actions, and auditable.

## Gray Conditions

- Action cost, side effect, duplicate prevention, approval boundary, limit boundary, monitoring, owner, data sensitivity, or automation capability unknown.

## Required Evidence

- Business rule owner.
- Workflow state enforcement.
- Idempotency.
- Quotas and caps.
- Rate-limit boundary.
- Monitoring.
- Abuse controls.
- Automation permissions.
- Cost/sensitivity classification.
- Current platform/tool behavior where relevant.

## Owners

Product owner, business owner, developer, operations owner, finance/fraud/risk owner, security owner, data owner, and AI governance owner.

## Non-Dev Action Checks

Do not remove approvals, raise limits, launch public forms, enable bulk exports, or automate high-impact actions until an owner confirms caps, approvals, audit logs, and monitoring. Use dry-run/review modes and least-privilege scopes.

## Unsafe Request Boundaries

Do not provide abuse playbooks, repeat counts, evasion details, or live testing instructions. Use defensive design review, synthetic scenarios, monitoring summaries, and owner-approved test fixtures.

## Safe Evidence Handling

Use workflow summaries, state diagrams, approval summaries, quota/cap summaries, monitoring summaries, synthetic examples, and owner confirmations. Do not include raw customer records or live abuse outputs.

## False-Positive Guardrails

Do not mark Green because a feature is "intended", "public", "rate limited", or "only manual" without confirming business boundary, actor, side effect, caps, monitoring, and owner approval.

## Under-Classification Guardrails

Treat repeatable costly actions, bulk exports, messaging triggers, public forms, support/admin overrides, and automation as Orange or Red when controls are unclear.

## Currentness Notes

Check current platform, vendor, payment, messaging, AI/no-code, and automation behavior when rate limits, costs, defaults, or abuse controls affect risk.

## Category Gate Rule

Fails on confirmed business-rule bypass, uncontrolled repeat/cost/resource/action amplification, sensitive bulk exposure, high-impact public flows, or unresolved abuse-control unknowns.
