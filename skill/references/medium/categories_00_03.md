# Medium Categories 00-03

Use this file with `medium_review.md`, `category_router.md`, and the shared references. Category detail here is stronger than Quick and less exhaustive than Indepth.

## 00. Review Governance, Scope, and Evidence Handling

Owns: Scope, authorization, evidence minimization, redaction, uncertainty handling, escalation, refusal boundaries, and pass/fail behavior.

Review focus: Is the review itself being performed safely, in scope, with current-source verification where material, redacted evidence, separated evidence/assumptions/unknowns, and required owner escalation?

Red:

- Raw or plausibly real secret/credential copied into evidence.
- Raw PII/private records copied outside approved scope.
- Request to use, test, replay, or open credential-like material.
- Unauthorized exploitation, bypass, scanning, enumeration, or unsafe validation request.
- Report repeats the exposure.
- Public or broad access exposes sensitive material.
- Production data or credentials used in lower-trust workflows without approval.
- Shared or weakened privileged access.
- Unapproved external, vendor, AI, or automation sharing of sensitive production material.

Orange:

- Credential type, restrictions, environment, or owner unknown in risky context.
- Sensitive data appears involved but classification or authorization is unknown.
- Vendor/support/AI/automation handling, retention, scopes, or approval unclear.
- Public/broad access or IAM scope has unknown sensitivity.
- Critical context is missing.
- Claims such as "internal", "staging", "test data", or "safe platform behavior" are unsupported.

Yellow:

- Incomplete redaction without raw sensitive exposure.
- Missing owner/approval path for low-risk evidence.
- Non-sensitive debug/logging/metadata exposure in controlled context.
- Safe public/publishable artifact lacks documentation.
- Evidence/assumption/unknown separation needs cleanup.

Green:

- Synthetic evidence.
- Fully redacted evidence.
- Documented publishable/restricted key or public client identifier.
- Intentionally public non-sensitive content.
- Approved vendor/tool integration with minimized evidence.
- Current-source assumptions verified where material.

Gray:

- Sensitivity, credential-like value, URL/link type, internal/staging/test claim, vendor/AI handling, broad access controls, or current vendor/cloud/browser/AI behavior is unknown.

Required evidence: Safe scope confirmation, redaction summary, current-source basis, owner path, sensitive-data category, environment, audience, approval status, and control summary.

Pass/fail: Fail on unsafe evidence handling, raw sensitive values, unsafe validation requests, or unresolved sensitive unknowns. Pass only when evidence is redacted, scope is authorized, currentness is addressed where material, and owner confirmations are complete.

## 01. Identity, Authentication, and Session Trust

Owns: User/service/device identity, login, signup, password reset, magic links, MFA, recovery, sessions, cookies, access/refresh/ID tokens, OAuth/OIDC/SAML, SSO, IdP settings, service accounts, workload identities, machine identities, vendor/contractor/support access, auth logs, and automation identity.

Review focus: Does the system authenticate actors safely and protect sessions, tokens, recovery paths, and identity state from misuse, exposure, takeover, or unsafe sharing?

Red:

- Missing authentication on sensitive/private/admin/production/vendor/support surfaces.
- Auth bypass or client-controlled identity trust.
- Live auth/session material exposed.
- Reset/recovery/MFA takeover path.
- MFA absent or bypassable for high-risk access.
- Uncontrolled high-impact session or refresh-token lifecycle.
- Invalidated session remains usable.
- Session fixation or reuse after auth.
- Uncontrolled shared high-risk account.
- Production credentials reused outside approved context.
- Federation misconfiguration.
- Unsafe identity mixing in automation or service accounts.

Orange:

- Unknown token-like value in risky location.
- Unknown cookie/session purpose.
- Unknown MFA for privileged/sensitive access.
- Unconfirmed federation, recovery strength, external access lifecycle, automation identity, temporary credential lifecycle, backend invalidation, or auth log safety.

Yellow:

- Lifecycle documentation gap.
- Low-risk auth logging improvement.
- Controlled MFA exception cleanup.
- Bounded remember-me/session issue.
- Service-account lifecycle tracking gap.
- Synthetic test identity hygiene gap.
- Auth attempt protection improvement.
- Redaction gap in auth screenshot.

Green:

- Public login/signup page without sensitive exposure.
- Confirmed public identity metadata.
- Secure session cookie attributes/lifecycle.
- Approved federation.
- Short-lived framework-managed tokens.
- Controlled remember-me.
- Approved machine identity.
- Synthetic isolated test accounts.
- Safe redacted auth evidence.

Gray:

- Token-like value, cookie/session role, MFA coverage, federation boundary, recovery assurance, external access lifecycle, automation identity, temporary credential lifecycle, backend invalidation, or auth log coverage unknown.

Required evidence: Auth boundary, session/token purpose, MFA/recovery posture, identity owner, lifecycle/invalidation, service-account scope, federation/trust boundary, and safe current platform/vendor docs where behavior matters.

Pass/fail: Fail when identity cannot be trusted, auth/session material is exposed, high-risk MFA/session/recovery is broken, shared privileged accounts are uncontrolled, or sensitive identity uncertainty remains unresolved.

## 02. Authorization, Access Control, and Trust Boundaries

Owns: Server-side authorization, RBAC/ABAC/ReBAC/ACLs, policy engines, object/function/property/record/tenant boundaries, API routes, query filters, dashboards, exports, files, storage permissions, admin/support/vendor/automation/AI access, sharing links, revocation, and access reviews.

Review focus: Are access decisions enforced by a trusted server-side or policy layer at every object, function, tenant, role, privilege, environment, public/private, and trust boundary?

Red:

- Confirmed cross-user/account/tenant/org/workspace exposure.
- Unauthorized privileged function access.
- Backend trusts client-controlled authorization values.
- Private data exposed through public/shared/signed link.
- Secondary-path authorization failure across list/view/preview/download/update/delete/export/search/cache/file paths.
- Self-service privilege escalation.
- Uncontrolled support impersonation/access.
- Sensitive revocation failure.
- Production/environment boundary failure.
- Broad AI/automation/service/CI/CD actor access causing unauthorized reach.

Orange:

- Suspected cross-boundary access.
- Server-side enforcement unknown.
- Frontend-only authorization possible.
- Client-supplied authorization values with unclear validation.
- Shared/public/signed-link controls unclear.
- Broad vendor/contractor/support/cloud/IAM/SaaS/storage/AI connector access unclear.
- Revocation, field/property auth, approval workflow, environment separation, or compliance-sensitive sharing uncertain.

Yellow:

- Permission matrix or role documentation incomplete.
- Low-risk overbroad access without sensitive/privileged impact.
- Lower-risk logging/review gap.
- Confusing role names with confirmed limited permissions.
- Shared-link hygiene for non-sensitive content.
- Frontend-control documentation gap with backend enforcement confirmed.

Green:

- Intentionally public non-sensitive resource.
- Frontend controls are UX-only with backend enforcement confirmed.
- Approved shared links or scoped signed URLs.
- Documented least-privilege policy model.
- Named admin/support/vendor access with strong controls.
- Isolated test accounts.
- Database row-level security/policy enforcement confirmed.

Gray:

- Route/button/link/menu, identifier, shared link, vendor access, broad role, dashboard/export/search/cache, API endpoint, query filter, support impersonation, internal-only claim, staging/test boundary, or AI/automation access exists but enforcement/scope is unknown.

Required evidence: Actor, resource, object/tenant/role boundary, trusted enforcement point, revocation behavior, sharing model, access logs, current platform behavior, and owner confirmation.

Pass/fail: Fail on unauthorized access, cross-boundary exposure, client-controlled authorization, uncontrolled privileged access, or unresolved sensitive authorization unknowns.

## 03. Sensitive Data, PII, and Privacy Boundaries

Owns: Collection, processing, storage, transmission, display, logging, export, retention, deletion, sharing, and tool/vendor/AI use of sensitive, personal, customer, employee, production, and confidential business data.

Review focus: Is sensitive data handled only where necessary, only by appropriate parties, with safe redaction, minimization, storage, sharing, retention, deletion, and review boundaries?

Red:

- Real sensitive data exposed outside approved scope.
- Public or link-accessible sensitive artifact.
- Cross-actor sensitive API/page exposure.
- Unapproved vendor/AI/automation processing.
- Production sensitive data in uncontrolled non-production workflow.
- Sensitive data leakage through logs, observability, or browser-visible surfaces.
- Tracking/session replay captures sensitive data.
- Raw sensitive evidence reproduced in review material.
- Unsafe retention after deletion or purpose end.

Orange:

- Likely sensitive exposure with missing origin/audience.
- Public/shared artifact with unknown sensitive content.
- External/tool processing controls unknown.
- Production-like data in lower-control workflow.
- Linkable dataset or identifier logging unresolved.
- Tracking on sensitive surface with unknown collection.
- Retention/deletion coverage or broad internal access unclear.
- Auditability for sensitive-data actions unresolved.

Yellow:

- Unnecessary identifiers in controlled internal logs.
- Non-sensitive over-return to authorized audience.
- Bounded retention documentation gap.
- Approved tool workflow needs minimization documentation.
- Controlled export lacks expiry/review cadence.
- Sensitive-looking metadata with limited visibility.
- Minor redaction improvement.

Green:

- Confirmed synthetic or approved demo data.
- Properly redacted evidence.
- Expected current-user self-service data.
- Approved role-limited internal access.
- Safe aggregate analytics.
- Approved third-party/AI/tool processing.
- Non-sensitive browser state.
- Expected public business information.

Gray:

- Data origin/sensitivity, realistic test-data origin, anonymization/de-identification claim, retention/deletion/tool/vendor/shared-link risk, or broad internal need-to-know controls unknown.

Required evidence: Data category, origin, audience, purpose, approval, minimization, retention/deletion, sharing path, vendor/AI settings, and current-source data/tool handling basis.

Pass/fail: Fail on confirmed sensitive-data exposure, unapproved external/tool processing, unsafe public sharing, raw sensitive evidence, uncontrolled production-data use, or unresolved sensitive-data unknowns.
