# 10. Configuration, Platform, Cloud, and Deployment Exposure

Category ID: 10

Category name: Configuration, Platform, Cloud, and Deployment Exposure

## Purpose

Review whether applications, services, infrastructure, hosting platforms, cloud resources, deployment environments, and operational settings expose more than they should because of configuration or deployment choices.

## Core Review Question

Is the system deployed with safe defaults, minimal public exposure, correct environment separation, appropriate platform/cloud controls, and no dangerous debug, admin, network, storage, or configuration exposure?

## Scope

Application/service/infrastructure/hosting/cloud/IaC/Kubernetes/Docker/serverless settings, environment separation, public/private exposure, networks, admin/debug/diagnostic surfaces, CORS/security headers/CDN/DNS/API gateway/WAF/cache, managed services, IAM/SaaS/vendor/no-code/AI permissions, preview deployments, artifacts, and drift.

## Review Signals

- Public/private exposure, environment, network, IAM, storage, debug/admin surface, CDN/cache/proxy/gateway, preview deployment, or deployment artifact affects sensitive data or production control.
- Non-production may contain production data, credentials, or capability.
- Provider default, current platform behavior, lifecycle/drift, or temporary exception is material.
- Broad cloud/IAM/vendor/automation permission exists.

## Red Conditions

- Public privileged management surface without effective restriction.
- Public production debug/diagnostic exposure with sensitive output.
- Public non-production environment containing production data or capability.
- Broad public network access to sensitive service without sufficient controls.
- Public storage, backup, snapshot, log, or artifact with sensitive material.
- CORS/edge/cache/proxy/gateway misconfiguration exposes sensitive authenticated/private content.
- Stale/dangling domain or deployment lifecycle issue creates serious exposure.
- Disabled critical WAF/private access/network/security control on sensitive production surface without approval or expiry.
- Broad cloud/IAM/vendor/automation permission gives unapproved production control or sensitive data access.
- Production/non-production credential, data, account, or network boundary failure.

## Orange Conditions

- Public/private exposure, environment, data sensitivity, upstream control, provider default, CORS/header/cache/DNS/IAM/network setting, lifecycle, current platform/cloud/vendor behavior, broad permission, or temporary exception lacks owner confirmation.

## Yellow Conditions

- Low-risk hardening, header, debug, environment lifecycle, artifact cleanup, permission documentation, or config drift issue with no sensitive exposure.
- Public/publishable non-sensitive resource lacks documentation.

## Green Conditions

- Resource intentionally public, non-sensitive, owner-approved, and separated from private systems.
- Privileged/admin surfaces private-network or identity restricted, MFA/least-privilege/audited.
- Non-production isolated with synthetic/approved data and separate credentials.
- Sensitive services use private endpoints, approved networks, or identity controls.
- Cloud/IAM/vendor access least-privilege, approved, time-limited where needed, and audited.

## Gray Conditions

- Exposure, sensitivity, environment, provider behavior, control ownership, effective permissions, lifecycle, or environment separation unknown.

## Required Evidence

- Environment.
- Exposure path.
- Network/IAM/storage/debug settings.
- Sensitive-data presence.
- Provider defaults and current docs.
- Owner approval.
- Lifecycle/drift status.
- Current exploitation/advisory context where applicable.

## Owners

Cloud/platform owner, DevOps/release owner, security owner, developer, infrastructure/network owner, identity owner, vendor owner, AI governance owner, and operations owner.

## Non-Dev Action Checks

Do not make resources public, open firewall rules broadly, disable protections, turn on debug mode publicly, or grant broad cloud access to make something work. Use scoped temporary access with approval, expiry, and logging.

## Unsafe Request Boundaries

Do not request private topology, account secrets, sensitive resource names, live private URLs, or instructions to probe exposure. Use redacted IaC/config summaries and owner-confirmed settings.

## Safe Evidence Handling

Use redacted config/IaC summaries, permission summaries, exposure summaries, environment descriptions, owner confirmations, current provider docs, and screenshots only after redaction.

## False-Positive Guardrails

Do not mark Green because a resource is "temporary", "staging", "hard to guess", "behind CDN", "internal", "provider-managed", or "only public briefly" without confirming exposure, sensitivity, approval, lifecycle, and controls.

## Under-Classification Guardrails

Treat public admin/debug surfaces, broad IAM, public storage, preview deployments, non-production with production-like data, and disabled controls as Orange or Red until owner and current provider context are clear.

## Currentness Notes

Check current cloud/platform/vendor defaults, security advisories, provider behavior, browser/CDN/cache behavior, and active exploitation when those facts affect risk or Green.

## Category Gate Rule

Fails on confirmed dangerous public/platform/cloud/deployment exposure, production boundary failure, broad unapproved permissions, unsafe debug/admin/network/storage exposure, or unresolved sensitive cloud/config unknowns.
