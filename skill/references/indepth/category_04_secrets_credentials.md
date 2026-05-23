# 04. Secrets, Credentials, and Key Management

Category ID: 04

Category name: Secrets, Credentials, and Key Management

## Purpose

Review whether secrets, credentials, keys, tokens, connection strings, signed URLs, service accounts, and related key material are exposed, overpowered, stored unsafely, shared unsafely, reused unsafely, or used in contexts where they should not exist.

## Core Review Question

Is any secret or credential exposed, overpowered, stored unsafely, shared unsafely, reused unsafely, or used in a context where it should not exist?

## Scope

Secrets, API keys, tokens, passwords, private/signing/encryption keys, connection strings, signed URLs, service accounts, secret managers, CI/CD/cloud/registry/deployment credentials, webhook secrets, OAuth/OIDC/SAML artifacts, recovery material, lifecycle, rotation, revocation, and publishability claims.

## Review Signals

- Token-like value, key-like value, private link, connection string, or credential appears in code, config, logs, screenshots, browser-visible content, tickets, artifacts, AI tools, vendor portals, or support workflows.
- Secret is claimed public, test, expired, local, fake, publishable, or already revoked without owner confirmation.
- Credential scope, owner, environment, storage, exposure audience, rotation, revocation, or logs/artifacts containing it are unclear.
- Service account, CI/CD, cloud, registry, or deployment credential has production or broad access.

## Red Conditions

- Production/privileged secret exposed outside approved controls.
- Secret or privileged key in client-visible context.
- Exposed cloud/service-account/CI/CD/deployment/registry credential with broad or production access.
- Credential committed to public/broad repo/artifact/package/image/backup without confirmed remediation.
- Secret disclosed through operations, support, vendor, AI, shared chat, ticket, or log channels.
- Identity/session/OAuth/OIDC/SAML/recovery/signing material exposed.
- Private/signing/encryption key or webhook secret exposed.
- Credential-bearing connection string exposed.
- Credential reuse across environments with production reach.
- Sensitive private access URL shared beyond intended audience.

## Orange Conditions

- Unknown token-like value in risky location.
- Frontend-visible key claimed public without proof.
- Repo/artifact/image/package secret with unclear reach.
- Operational secret leakage audience or retention unclear.
- Machine credential scope, owner, lifecycle, or storage unclear.
- Test/staging/local/expired/revoked/placeholder claim unverified.
- Shared human credential or personal admin token.
- Third-party/AI/no-code/automation credential uncertainty.
- Rotation/revocation unclear.
- Credential evidence mixed with sensitive data.

## Yellow Conditions

- Credential ownership, rotation, lifecycle, restriction, quota, remediation, audit, or approved vendor/automation documentation incomplete.
- Non-usable credential indicators in logs/reports need cleanup.
- Low-risk secret scanning or inventory gap.

## Green Conditions

- Documented restricted publishable key.
- Public client ID or non-secret config.
- Clearly fake placeholder.
- Local-only test credential isolated from production and real data.
- Approved protected secret handling.
- Controlled machine credential workflow.
- Controlled CI/CD secret handling.
- Safe redacted evidence.
- Controlled private link sharing.

## Gray Conditions

- Token-like value, public/test claim, connection string/config reference, browser token, third-party/vendor/no-code/AI credential behavior, or private link behavior has insufficient context.

## Required Evidence

- Secret type without value.
- Environment, scope, permissions, storage mechanism, and owner.
- Rotation/revocation status.
- Exposure audience.
- Logs, artifacts, repositories, images, packages, or browser contexts containing it.
- Current vendor/platform docs for publishability or secret behavior.

## Owners

Security owner, developer, identity owner, cloud/platform owner, DevOps/release owner, vendor owner, AI governance owner, and operations owner.

## Non-Dev Action Checks

Do not paste, screenshot, forward, upload, decode, test, or store secrets in chat, spreadsheets, tickets, AI tools, public pages, or vendor portals. Use approved secret storage, backend flows, scoped service accounts, and rotation/revocation when exposure is plausible.

## Unsafe Request Boundaries

Do not request or validate raw secrets, decode tokens, test credentials, open signed links, use private URLs, or ask for credential values. Ask for redacted type, location, environment, scope, owner, and lifecycle status.

## Safe Evidence Handling

Use placeholders and safe summaries. Preserve only type, location, exposure surface, environment, audience, known controls, owner, and required action.

## False-Positive Guardrails

Do not mark Green because a key is "probably public", "probably expired", "only staging", "local", "redacted enough", or "already rotated" without owner confirmation and current vendor behavior when needed.

## Under-Classification Guardrails

Treat visible tokens, bearer strings, connection strings, signed URLs, service account material, and OAuth/SAML artifacts as Orange or Red until purpose, scope, audience, and lifecycle are safely confirmed.

## Currentness Notes

Check current vendor docs for publishable keys, token behavior, key restrictions, signed URL behavior, secret scanning behavior, and revocation/rotation guidance when these facts affect Green or remediation.

## Category Gate Rule

Fails on confirmed real or likely live secret exposure, unsafe credential storage/sharing/use, production credential misuse, or unknown high-risk credential context that remains unresolved.
