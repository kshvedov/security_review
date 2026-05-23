# Medium Categories 08-11

Use this file with `medium_review.md`, `category_router.md`, and the shared references. Category detail here is stronger than Quick and less exhaustive than Indepth.

## 08. File, Object, Content, and Storage Handling

Owns: Files, uploads, downloads, attachments, generated content, documents, media, archives, backups, object/blob storage, buckets/folders/ACL/IAM, signed/pre-signed/SAS URLs, shared links, previews, rendering, indexing, OCR, conversion, metadata, caches, CDN mirrors, and vendor/AI/no-code/support file workflows.

Review focus: Are files, objects, storage locations, generated content, uploads, downloads, previews, and shared content protected with correct access control, safe processing, safe storage, safe metadata handling, and safe exposure boundaries?

Red:

- Sensitive private files/objects publicly accessible.
- Public listing exposes sensitive files/names/storage structure.
- Backups, dumps, logs, source archives, or old exports public or broadly shared.
- Generated files include wrong-scope or excessive sensitive data.
- File operation crosses ownership or permission boundaries.
- Secrets/credentials exposed through files, artifacts, storage, links, or logs.
- Signed/shared/access-granting links expose sensitive content beyond intended audience.
- Unsafe upload/file processing path handles untrusted content with sensitive impact.
- Private file cache/CDN/preview mirror remains accessible after revocation.
- Sensitive files sent to unapproved vendor/AI/no-code/support workflow.

Orange:

- Public/broad file or storage access with unknown contents/approval.
- Signed link scope, expiry, revocation, or logging unknown.
- Upload/download/preview/archive/conversion controls unknown.
- Generated file scoping unknown.
- Backup/artifact/log contents and retention unclear.
- Vendor/AI/support file handling unknown.

Yellow:

- Non-sensitive file listing/storage metadata hygiene issue.
- Controlled signed link lacks documentation or expiry review.
- Low-risk upload/scanning documentation gap.
- Private cache/retention rationale needs documentation.
- File metadata minimization improvement.

Green:

- Intentionally public non-sensitive approved static/marketing content.
- Private files access-controlled, least-privilege, audited, and retained appropriately.
- Signed links scoped, short-lived, revocable, auditable, and intended-recipient only.
- Uploads authenticated/authorized, limited, isolated, scanned where needed, and safely served.
- Untrusted processing isolated/resource-limited.
- Generated exports correctly scoped and retained.

Gray:

- File sensitivity, access audience, link controls, upload/processing isolation, cache behavior, generated-file scope, vendor/tool handling, or artifact contents unknown.

Required evidence: File/data category, access audience, object/storage policy, link expiry/revocation, processing path, cache/CDN behavior, generated-file scoping, retention, vendor/tool handling, and current provider behavior.

Pass/fail: Fail on public/broad sensitive file exposure, wrong-scope generated files, unsafe file operations, exposed credential-bearing artifacts, or unresolved sensitive storage/link/file-processing unknowns.

## 09. Business Logic, Abuse Prevention, and Resource Controls

Owns: Intended feature misuse, workflow integrity, state transitions, approvals, checkout/billing/refunds/credits/discounts/coupons/trials/referrals/entitlements/quotas, signup/invite/account-existence flows, public forms/links/webhooks, exports/search/sync/bulk actions/background jobs, messaging triggers, rate limits, quotas, cost controls, AI/no-code/vendor automation, and admin/support/finance/operations overrides.

Review focus: Can someone use allowed features in an unintended way to bypass rules, abuse resources, cause operational harm, or create business/security impact?

Red:

- Unbounded repeatable sensitive or costly workflow.
- Workflow order, approval, state, or separation-of-duties bypass with serious impact.
- Client-controlled business-critical value affects authoritative outcome.
- Public unauthenticated flow triggers high-impact, costly, external, or sensitive side effects without meaningful controls.
- Bulk export/search/report/sync exposes sensitive data without limits, approval, or audit.
- High-volume messaging/invite/notification/webhook trigger lacks caps, suppression, or monitoring.
- Expensive operation repeatable at high volume without controls.
- Admin/support override bypasses high-risk controls without approval, audit, or expiry.
- AI/automation amplifies high-impact actions without approval, limits, or logging.

Orange:

- Potentially repeatable/costly/sensitive flow with duplicate prevention, idempotency, quotas, monitoring, approval, or business owner unknown.
- Public forms, bulk exports, message triggers, AI/tool costs, or override paths have unclear controls.
- Rate limit boundary may not match the business entity at risk.

Yellow:

- Low-risk workflow/quota documentation gap.
- Minor alerting, monitoring, or rate-limit tuning issue.
- Controlled override/access path needs expiry or review cadence.
- Abuse scenario should be ticketed but is not a current blocker.

Green:

- Retries idempotent, bounded, monitored, and owner-approved.
- Workflow states and approvals enforced server-side with audit logs.
- Business-critical values recomputed or validated server-side.
- Public flows validated, rate-limited, monitored, low-impact, and approved.
- Bulk access role-limited, logged, capped, approved, and aligned to sensitivity.
- Automation least-privilege, capped, human-confirmed for sensitive actions, and auditable.

Gray:

- Action cost, side effect, duplicate prevention, approval boundary, limit boundary, monitoring, owner, data sensitivity, or automation capability unknown.

Required evidence: Business rule owner, workflow state enforcement, idempotency, quotas/caps, rate-limit boundary, monitoring, abuse controls, automation permissions, cost/sensitivity classification, and current platform/tool behavior where relevant.

Pass/fail: Fail on business-rule bypass, uncontrolled repeat/cost/resource/action amplification, sensitive bulk exposure, high-impact public flows, or unresolved abuse-control unknowns.

## 10. Configuration, Platform, Cloud, and Deployment Exposure

Owns: Application/service/infrastructure/hosting/cloud/IaC/Kubernetes/Docker/serverless settings, environment separation, public/private exposure, networks, admin/debug/diagnostic surfaces, CORS/security headers/CDN/DNS/API gateway/WAF/cache, managed services, IAM/SaaS/vendor/no-code/AI permissions, preview deployments, artifacts, and drift.

Review focus: Is the system deployed with safe defaults, minimal public exposure, correct environment separation, appropriate platform/cloud controls, and no dangerous debug, admin, network, storage, or configuration exposure?

Red:

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

Orange:

- Public/private exposure, environment, data sensitivity, upstream control, provider default, CORS/header/cache/DNS/IAM/network setting, lifecycle, current platform/cloud/vendor behavior, broad permission, or temporary exception lacks owner confirmation.

Yellow:

- Low-risk hardening, header, debug, environment lifecycle, artifact cleanup, permission documentation, or config drift issue with no sensitive exposure.
- Public/publishable non-sensitive resource lacks documentation.

Green:

- Resource intentionally public, non-sensitive, owner-approved, and separated from private systems.
- Privileged/admin surfaces private-network or identity restricted, MFA/least-privilege/audited.
- Non-production isolated with synthetic/approved data and separate credentials.
- Sensitive services use private endpoints, approved networks, or identity controls.
- Cloud/IAM/vendor access least-privilege, approved, time-limited where needed, and audited.

Gray:

- Exposure, sensitivity, environment, provider behavior, control ownership, effective permissions, lifecycle, or environment separation unknown.

Required evidence: Environment, exposure path, network/IAM/storage/debug settings, sensitive-data presence, provider defaults/current docs, owner approval, lifecycle/drift status, and current exploitation/advisory context where applicable.

Pass/fail: Fail on dangerous public/platform/cloud/deployment exposure, production boundary failure, broad unapproved permissions, unsafe debug/admin/network/storage exposure, or unresolved sensitive cloud/config unknowns.

## 11. Dependencies, Build, CI/CD, and Supply Chain Integrity

Owns: Dependency manifests, lockfiles, package sources, registries, SCA/SBOM/container/secret scans, build/install/test/codegen scripts, CI/CD workflows/runners/triggers/permissions/secrets/approvals, repo/branch/tag/release/publishing controls, logs/artifacts/images/source maps/rollback bundles, vendor apps/bots/service accounts/no-code/AI deployment automations, generated/vendored/copied/submodule code.

Review focus: Are dependencies, packages, build steps, CI/CD workflows, artifact stores, deployment pipelines, and release controls trusted, least-privilege, auditable, reproducible where needed, and protected from unsafe modification or exposure?

Red:

- Exposed production CI/CD, deployment, registry, cloud, signing, or package-publish secret.
- Untrusted workflow path can access secrets, write permissions, deployment, signing, or package publishing.
- Sensitive material included in published/deployable artifacts.
- Unauthorized or unaudited production deployment, release, tag, workflow modification, or package publishing capability.
- Confirmed dependency confusion or unsafe registry resolution affecting trusted builds.
- Privileged build/install/codegen step executes untrusted remote code.
- Reachable known exploited or high-impact vulnerable dependency in production without mitigation.
- Untrusted self-hosted runner exposes secrets or internal network.
- Unreviewed generated, copied, vendored, submodule, or AI-generated code with sensitive or production impact.

Orange:

- Dependency reachability, production inclusion, or current advisory status unclear.
- CI/CD trigger, permission, secret exposure, or deployment scope unclear.
- Third-party action, plugin, app, bot, or integration trust unknown.
- Artifact, image, source map, SBOM, or release content/access unclear.
- Registry/private namespace controls unclear.
- Signing, provenance, or integrity controls absent where needed.
- Generated/vendored/copied/submodule/AI code review or ownership unclear.
- Deployment automation from personal, local, shared, or unmanaged path has uncertain production impact.

Yellow:

- Outdated dependency with limited exposure and missing tracking.
- Missing or inconsistent lockfile/reproducibility control in low-risk context.
- Minor non-sensitive build/test/deployment log exposure.
- Low-risk scan triage gap.
- Controlled build script documentation gap.
- Container image hygiene issue without high-risk contents.
- Vulnerability exception needs expiry, owner, or review cadence.
- Controlled vendor/bot/service-account access documentation incomplete.

Green:

- Dependencies pinned/locked/reviewed and sourced from trusted registries.
- Vulnerability not reachable or mitigated with owner confirmation.
- CI/CD least-privilege with isolated secrets, reviewed triggers, and protected deploy gates.
- Artifacts/images/source maps/logs scanned and access-controlled.
- Release controls enforce review, approval, provenance, and auditability.
- Third-party actions/apps/bots are pinned, scoped, reviewed, and revocable.
- Generated/copied/AI code reviewed before production use.

Gray:

- Dependency identity, version, source, reachability, deployment path, advisory status, CI/CD permissions, artifact contents, registry controls, runner trust, generated code ownership, or exception status unknown.

Required evidence: Dependency identity/version/source/reachability, current advisory/CVE/KEV/vendor status, deployment path, CI/CD permissions/secrets, runner trust, artifact contents, registry controls, provenance/signing, review ownership, and exception/mitigation status.

Pass/fail: Fail on supply-chain secret exposure, untrusted privileged workflows, sensitive artifacts, unauthorized deploy/publish capability, unsafe registry resolution, or reachable unmitigated high-impact dependency.
