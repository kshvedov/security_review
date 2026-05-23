# 11. Dependencies, Build, CI/CD, and Supply Chain Integrity

Category ID: 11

Category name: Dependencies, Build, CI/CD, and Supply Chain Integrity

## Purpose

Review whether dependencies, packages, build steps, CI/CD workflows, artifact stores, deployment pipelines, generated code, release controls, and publishing paths are trusted, least-privilege, auditable, reproducible where needed, and protected from unsafe modification or exposure.

## Core Review Question

Are dependencies, packages, build steps, CI/CD workflows, artifact stores, deployment pipelines, and release controls trusted, least-privilege, auditable, reproducible where needed, and protected from unsafe modification or exposure?

## Scope

Dependency manifests, lockfiles, package sources, registries, SCA/SBOM/container/secret scans, build/install/test/codegen scripts, CI/CD workflows/runners/triggers/permissions/secrets/approvals, repo/branch/tag/release/publishing controls, logs/artifacts/images/source maps/rollback bundles, vendor apps/bots/service accounts/no-code/AI deployment automations, generated/vendored/copied/submodule code.

## Review Signals

- Dependency source, version, registry, lockfile, package manager config, private namespace, or install/build script affects trusted code resolution.
- CI/CD workflow, trigger, runner, secret, artifact, deploy gate, release, package publishing, or third-party action has privileged access.
- Artifact, image, source map, release bundle, SBOM, or log may contain sensitive material.
- Generated, copied, vendored, submodule, or AI-generated code enters production.
- Advisory, CVE, KEV, reachability, exploitability, or mitigation status is currentness-sensitive.

## Red Conditions

- Exposed production CI/CD, deployment, registry, cloud, signing, or package-publish secret.
- Untrusted workflow path can access secrets, write permissions, deployment, signing, or package publishing.
- Sensitive material included in published/deployable artifacts.
- Unauthorized or unaudited production deployment, release, tag, workflow modification, or package publishing capability.
- Confirmed dependency confusion or unsafe registry resolution affecting trusted builds.
- Privileged build/install/codegen step executes untrusted remote code.
- Reachable known exploited or high-impact vulnerable dependency in production without mitigation.
- Untrusted self-hosted runner exposes secrets or internal network.
- Unreviewed generated, copied, vendored, submodule, or AI-generated code with sensitive or production impact.

## Orange Conditions

- Dependency reachability, production inclusion, or current advisory status unclear.
- CI/CD trigger, permission, secret exposure, or deployment scope unclear.
- Third-party action, plugin, app, bot, or integration trust unknown.
- Artifact, image, source map, SBOM, or release content/access unclear.
- Registry/private namespace controls unclear.
- Signing, provenance, or integrity controls absent where needed.
- Generated/vendored/copied/submodule/AI code review or ownership unclear.
- Deployment automation from personal, local, shared, or unmanaged path has uncertain production impact.

## Yellow Conditions

- Outdated dependency with limited exposure and missing tracking.
- Missing or inconsistent lockfile/reproducibility control in low-risk context.
- Minor non-sensitive build/test/deployment log exposure.
- Low-risk scan triage gap.
- Controlled build script documentation gap.
- Container image hygiene issue without high-risk contents.
- Vulnerability exception needs expiry, owner, or review cadence.
- Controlled vendor/bot/service-account access documentation incomplete.

## Green Conditions

- Dependencies pinned/locked/reviewed and sourced from trusted registries.
- Vulnerability not reachable or mitigated with owner confirmation.
- CI/CD least-privilege with isolated secrets, reviewed triggers, and protected deploy gates.
- Artifacts/images/source maps/logs scanned and access-controlled.
- Release controls enforce review, approval, provenance, and auditability.
- Third-party actions/apps/bots are pinned, scoped, reviewed, and revocable.
- Generated/copied/AI code reviewed before production use.

## Gray Conditions

- Dependency identity, version, source, reachability, deployment path, advisory status, CI/CD permissions, artifact contents, registry controls, runner trust, generated code ownership, or exception status unknown.

## Required Evidence

- Dependency identity, version, source, and reachability.
- Current advisory/CVE/KEV/vendor status where material.
- Deployment path.
- CI/CD permissions and secrets.
- Runner trust.
- Artifact contents.
- Registry controls.
- Provenance/signing.
- Review ownership.
- Exception/mitigation status.

## Owners

Developer, DevOps/release owner, security owner, cloud/platform owner, vendor owner, AI governance owner, and operations owner.

## Non-Dev Action Checks

Do not install unapproved plugins/actions, bypass reviews, share build logs with secrets, publish artifacts with unknown contents, or deploy from personal/shared credentials. Route through approved CI/CD and owner review.

## Unsafe Request Boundaries

Do not include malicious package examples, exploit details, secrets from build logs, private package paths when sensitive, or instructions to test live compromise. Use safe dependency metadata, redacted logs, scan summaries, and owner-confirmed reachability.

## Safe Evidence Handling

Use redacted dependency manifests, lockfile summaries, CI/CD permission summaries, artifact scan summaries, SBOM summaries, source-map access summaries, and current official advisories.

## False-Positive Guardrails

Do not mark Green because a dependency is "probably not reachable", a CI job is "internal", a third-party action is "popular", or an artifact is "temporary" without reachability, permissions, artifact contents, and owner confirmation.

## Under-Classification Guardrails

Treat privileged workflow triggers, write/deploy/publish/sign permissions, self-hosted runners, generated code, source maps, broad bots, and current exploited vulnerabilities as Orange or Red until context is clear.

## Currentness Notes

Check current advisories, CVE/NVD, KEV, vendor/project security advisories, release notes, package registry behavior, CI/CD platform behavior, and exploit status where material.

## Category Gate Rule

Fails on secret exposure in supply chain, untrusted privileged workflows, sensitive artifacts, unauthorized deploy/publish capability, unsafe registry resolution, or reachable unmitigated high-impact dependency.
