# 02. Authorization, Access Control, and Trust Boundaries

Category ID: 02

Category name: Authorization, Access Control, and Trust Boundaries

## Purpose

Review whether authenticated users, roles, tenants, services, vendors, contractors, admins, support users, automated actors, and public visitors can access only the objects, functions, data, environments, and actions they are allowed to access.

## Core Review Question

Are access decisions enforced server-side or by another trusted policy layer at every object, function, tenant, role, privilege, environment, public/private, and trust boundary?

## Scope

Server-side authorization, RBAC/ABAC/ReBAC/ACLs, policy engines, object/function/property/record/tenant boundaries, API routes, query filters, dashboards, exports, files, storage permissions, admin/support/vendor/automation/AI access, sharing links, revocation, and access reviews.

## Review Signals

- User, tenant, account, org, workspace, object, file, report, export, or dashboard boundaries are involved.
- Client or frontend appears to provide role, tenant, user, group, scope, or authorization-critical values.
- A secondary path such as preview, download, export, search, cache, report, webhook, support tool, or admin route may bypass the main authorization path.
- Shared links, signed links, vendor access, support impersonation, service accounts, or AI connectors reach private resources.
- Revocation, ownership transfer, account disablement, or environment separation may be incomplete.

## Red Conditions

- Confirmed cross-user/account/tenant/org/workspace exposure.
- Unauthorized privileged function access.
- Backend trusts client-controlled authorization values.
- Private data exposed through public/shared/signed link.
- Secondary-path authorization failure across list/view/preview/download/update/delete/export/search/cache/file paths.
- Self-service privilege escalation.
- Uncontrolled support impersonation or access.
- Sensitive revocation failure.
- Production/environment boundary failure.
- Broad AI/automation/service/CI/CD actor access causing unauthorized reach.

## Orange Conditions

- Suspected cross-boundary access.
- Server-side enforcement unknown.
- Frontend-only authorization possible.
- Client-supplied authorization values with unclear validation.
- Shared/public/signed-link controls unclear.
- Broad vendor/contractor/support/cloud/IAM/SaaS/storage/AI connector access unclear.
- Revocation, field/property authorization, approval workflow, environment separation, or compliance-sensitive sharing uncertain.

## Yellow Conditions

- Permission matrix or role documentation incomplete.
- Low-risk overbroad access without sensitive/privileged impact.
- Lower-risk logging or review gap.
- Confusing role names with confirmed limited permissions.
- Shared-link hygiene for non-sensitive content.
- Frontend-control documentation gap with backend enforcement confirmed.

## Green Conditions

- Intentionally public non-sensitive resource.
- Frontend controls are UX-only with backend enforcement confirmed.
- Approved shared links or scoped signed URLs.
- Documented least-privilege policy model.
- Named admin/support/vendor access with strong controls.
- Isolated test accounts.
- Database row-level security or policy enforcement confirmed.

## Gray Conditions

- Route/button/link/menu, identifier, shared link, vendor access, broad role, dashboard/export/search/cache, API endpoint, query filter, support impersonation, internal-only claim, staging/test boundary, or AI/automation access exists but enforcement/scope is unknown.

## Required Evidence

- Actor, resource, and action.
- Object, tenant, role, and trust boundary.
- Trusted enforcement point.
- Revocation behavior.
- Sharing model.
- Access logs.
- Current platform behavior where relevant.
- Owner confirmation.

## Owners

Developer, security owner, identity owner, data owner, product owner, vendor owner, cloud/platform owner, operations owner, and AI governance owner.

## Non-Dev Action Checks

Do not make a private resource public or share admin/report/file links broadly. Use named least-privilege access, expiry/revocation, and owner-approved sharing. Do not prove risk by accessing someone else's data.

## Unsafe Request Boundaries

Do not ask the user to change IDs, access another account, enumerate users, open private links, or prove authorization failure against real data. Use synthetic fixtures, owner-confirmed permissions, and redacted policy summaries.

## Safe Evidence Handling

Use redacted summaries, synthetic examples, local-only fixtures, architecture descriptions, safe configuration summaries, permission summaries, owner confirmations, and current official documentation when provider behavior matters.

## False-Positive Guardrails

Do not mark Green because a control is hidden in the frontend, a URL is hard to guess, a role is called admin, or access is "internal". Require trusted enforcement and need-to-know confirmation.

## Under-Classification Guardrails

Treat public/shared/signed links, broad service roles, vendor/support access, and unclear revocation as Orange or Gray when sensitive resources may be reachable.

## Currentness Notes

Check current platform, cloud IAM, SaaS sharing, signed-link, storage, RAG/source authorization, and vendor access behavior when those facts determine safety.

## Category Gate Rule

Fails on confirmed unauthorized access, cross-boundary exposure, client-controlled authorization, uncontrolled privileged access, or unresolved sensitive authorization unknowns.
