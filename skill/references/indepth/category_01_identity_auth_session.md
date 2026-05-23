# 01. Identity, Authentication, and Session Trust

Category ID: 01

Category name: Identity, Authentication, and Session Trust

## Purpose

Review whether users, services, devices, automated workflows, and other actors are correctly identified and whether authentication and session state are established, protected, maintained, and invalidated safely.

## Core Review Question

Does the system authenticate actors safely and protect sessions, tokens, recovery paths, and identity state from misuse, exposure, takeover, or unsafe sharing?

## Scope

Login, signup, password reset, magic links, MFA, recovery, sessions, cookies, access/refresh/ID tokens, OAuth/OIDC/SAML, SSO, IdP settings, service accounts, workload identities, machine identities, vendor/contractor/support access, authentication logs, and AI/browser automation identity.

## Review Signals

- Sensitive/admin/production/vendor/support surface may be reachable without verified authentication.
- Client-side values appear to affect authentication state.
- Authentication/session material appears in unsafe locations such as URLs, browser storage, logs, screenshots, tickets, AI tools, or vendor tooling.
- MFA coverage, reset/recovery, account recovery, or session invalidation is weak or unclear.
- Shared accounts, production credentials outside approved context, federation/SSO settings, service accounts, or automation identities are broad or unowned.
- Authentication event logs are missing, unsafe, or not reviewable.

## Red Conditions

- Missing authentication on sensitive/private/admin/production/vendor/support surfaces.
- Confirmed authentication bypass or client-controlled identity trust.
- Confirmed exposure of live authentication or session material.
- Account recovery, password reset, magic link, or MFA reset takeover path.
- MFA absent or bypassable for confirmed high-risk access.
- Uncontrolled high-impact session or refresh-token lifecycle.
- Sensitive session state remains valid after invalidation events.
- Session fixation or session identifier reuse after authentication.
- Uncontrolled shared high-risk account.
- Production credentials reused outside approved production context.
- Federation misconfiguration enabling unintended identity trust.
- Unsafe identity type mixing in automation or service accounts.

## Orange Conditions

- Unknown token-like value in risky location.
- Unknown cookie purpose or session sensitivity.
- Unknown MFA status for privileged/sensitive access.
- Unconfirmed federation configuration, recovery strength, external access lifecycle, automation identity, temporary credential lifecycle, backend invalidation, or auth log safety.

## Yellow Conditions

- Incomplete lifecycle documentation.
- Low-risk auth logging improvement.
- Controlled MFA exception cleanup.
- Bounded remember-me/session persistence issue.
- Service account lifecycle tracking gap.
- Synthetic test identity hygiene gap.
- Authentication attempt protection improvement.
- Evidence redaction gap in auth screenshot.

## Green Conditions

- Public login/signup pages with no sensitive exposure.
- Confirmed public identity metadata.
- Secure session cookie attributes and lifecycle.
- Approved federation integration.
- Short-lived framework-managed tokens.
- Controlled remember-me flow.
- Approved machine identity.
- Synthetic isolated test accounts.
- Safe redacted auth evidence.

## Gray Conditions

- Unknown token-like value, cookie/session role, MFA coverage, federation boundaries, recovery assurance, external access lifecycle, automation identity type, temporary credential lifecycle, backend invalidation, or auth log coverage.

## Required Evidence

- Auth boundary and enforcement point.
- Session/token purpose and lifecycle.
- MFA/recovery posture.
- Identity owner.
- Invalidation behavior.
- Service-account scope.
- Federation/trust boundary.
- Safe current platform/vendor documentation where behavior matters.

## Owners

Developer, security owner, identity owner, cloud/platform owner, vendor owner, DevOps/release owner, support/operations owner, and privacy owner.

## Non-Dev Action Checks

Do not share passwords, reset links, MFA/recovery codes, session cookies, tokens, or screenshots with visible identities. Use named accounts with MFA, approved service identities, and redacted setting summaries.

## Unsafe Request Boundaries

Do not ask the user to validate tokens, open reset links, provide MFA/recovery codes, test another user's session, or prove access by entering private accounts. Use redacted settings summaries, owner confirmation, synthetic accounts, and authorized test fixtures.

## Safe Evidence Handling

Use redacted summaries, synthetic examples, local-only fixtures, architecture descriptions, safe configuration summaries, permission summaries, owner confirmations, and current official documentation when provider behavior matters.

## False-Positive Guardrails

Do not mark Green only because a page is "internal", a token is "probably expired", MFA is "standard", or SSO is "managed". Require owner-confirmed settings and lifecycle.

## Under-Classification Guardrails

Treat unknown session material, recovery flows, shared accounts, temporary credentials, automation identities, and privileged access as Orange or Gray until scope and owner controls are confirmed.

## Currentness Notes

Check current IdP, OAuth/OIDC/SAML, session, browser cookie, vendor support-access, and platform behavior when the outcome depends on current external behavior.

## Category Gate Rule

Fails when identity cannot be trusted, session/auth material is exposed, high-risk MFA/session/recovery is broken, shared privileged accounts are uncontrolled, or sensitive authentication uncertainty remains unresolved.
