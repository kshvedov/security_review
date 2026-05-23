# Medium Categories 04-07

Use this file with `medium_review.md`, `category_router.md`, and the shared references. Category detail here is stronger than Quick and less exhaustive than Indepth.

## 04. Secrets, Credentials, and Key Management

Owns: Secrets, credentials, keys, tokens, connection strings, signed URLs, service accounts, secret managers, private/signing/encryption keys, CI/CD secrets, registry/cloud/deployment credentials, webhook secrets, and lifecycle management.

Review focus: Is any secret or credential exposed, overpowered, stored unsafely, shared unsafely, reused unsafely, or used in a context where it should not exist?

Red:

- Production/privileged secret exposed outside approved controls.
- Secret or privileged key in client-visible context.
- Exposed cloud/service-account/CI/CD/deployment/registry credential with broad or production access.
- Credential committed to public/broad repo/artifact/package/image/backup without confirmed remediation.
- Secret disclosed through operations/support/vendor/AI/shared channels.
- Identity/session/OAuth/OIDC/SAML/recovery/signing material exposed.
- Private/signing/encryption key or webhook secret exposed.
- Credential-bearing connection string exposed.
- Credential reuse across environments with production reach.
- Sensitive private access URL shared beyond intended audience.

Orange:

- Unknown token-like value in risky location.
- Frontend-visible key claimed public without proof.
- Repo/artifact/image/package secret with unclear reach.
- Operational secret leakage audience/retention unclear.
- Machine credential scope, owner, lifecycle, or storage unclear.
- Test/staging/local/expired/revoked/placeholder claim unverified.
- Shared human credential or personal admin token.
- Third-party/AI/no-code/automation credential uncertainty.
- Rotation/revocation unclear.
- Credential evidence mixed with sensitive data.

Yellow:

- Credential ownership, rotation, lifecycle, restriction, quota, remediation, audit, or approved vendor/automation documentation incomplete.
- Non-usable credential indicators in logs/reports need cleanup.

Green:

- Documented restricted publishable key.
- Public client ID or non-secret config.
- Clearly fake placeholder.
- Local-only test credential isolated from production and real data.
- Approved protected secret handling.
- Controlled machine credential workflow.
- Controlled CI/CD secret handling.
- Safe redacted evidence.
- Controlled private link sharing.

Gray:

- Token-like value, public/test claim, connection string/config reference, browser token, third-party/vendor/no-code/AI credential behavior, or private link behavior has insufficient context.

Required evidence: Secret type without value, environment, scope, permissions, storage mechanism, owner, rotation/revocation status, exposure audience, logs/artifacts containing it, and current vendor/platform docs for publishability or secret behavior.

Pass/fail: Fail on confirmed real or likely live secret exposure, unsafe credential storage/sharing/use, production credential misuse, or unresolved high-risk credential unknowns.

## 05. Input, Query, and Execution Safety

Owns: Untrusted, external, file-derived, AI-generated, user-controlled, or workflow-provided input affecting queries, execution, rendering, routing, paths, commands, templates, redirects, backend requests, parsers, or trusted behavior.

Review focus: Are untrusted inputs validated, constrained, encoded, parameterized, escaped, parsed, and handled before they affect queries, execution, rendering, paths, destinations, or sensitive backend behavior?

Red:

- Untrusted input directly controls production/sensitive query logic without confirmed parameterization or allowlisted structure.
- Input controls command/shell/subprocess/script execution without strict controls.
- Input reaches eval-like execution or dynamic loading without isolation.
- Unsafe deserialization/parser behavior in production or sensitive context.
- Input-controlled backend request destination crosses internal/cloud/privileged boundaries.
- Input-controlled file/object/include/template path reaches sensitive resources.
- Input-controlled redirect/callback creates sensitive workflow risk.
- Untrusted rendered content becomes active content in sensitive user/admin context.
- Unverified webhook/external payload triggers privileged logic.
- AI/no-code/generated output acts on production/sensitive systems without review.

Orange:

- Source/sink/control status incomplete for sensitive query, command, template, path, destination, parser, webhook, AI/no-code, or automation flow.
- Client/workflow controls structural fields, operators, or destinations but mapping is unclear.
- Generated code/query/script/formula review unknown.
- Logs/screenshots may contain sensitive input-derived values.

Yellow:

- Low-risk validation, documentation, sanitizer policy, schema, parser setting, redirect mapping, or review-process gap with no sensitive or production impact.
- Controlled generated output needs ticketed review documentation.
- Minor redaction cleanup.

Green:

- Values parameterized and structural parts server-side allowlisted.
- Output encoded/sanitized for exact context.
- Commands use fixed operations with separated allowlisted arguments and least privilege.
- Destinations/paths server-generated or allowlisted with boundary checks.
- Webhooks verified, schema-validated, freshness/replay-controlled, and least-privilege mapped.
- Generated outputs are advisory or owner-reviewed before use.

Gray:

- Input source, sink, environment, sensitivity, structural control, sanitizer policy, parser setting, webhook verification, or generated-output review unknown.

Required evidence: Input source, sink, data/control separation, validation/allowlist, encoding/parameterization, parser/deserialization controls, privilege boundary, review status, and current framework/library behavior where relevant.

Pass/fail: Fail on untrusted input reaching high-risk sinks without controls or unresolved input-safety unknowns affecting sensitive data, production systems, privileged actions, or external sharing.

## 06. API, Service, and Integration Boundaries

Owns: APIs, backend services, internal/external services, webhooks, callbacks, partner connections, no-code integrations, automation connectors, machine-to-machine workflows, schemas, scopes, limits, errors, logs, inventory, and vendor integrations.

Review focus: Is the API, service, webhook, callback, connector, automation, or integration boundary safe to expose, call, trust, consume, or connect for the data and actions it handles?

Red:

- Unauthorized sensitive API data exposure.
- Privileged API action exposed without confirmed server-side authorization.
- Live API/integration credential exposed.
- Restricted/private/admin/debug/staging/internal/deprecated API publicly reachable with sensitive impact.
- Unapproved third-party/no-code/automation/AI access to sensitive production APIs.
- Sensitive webhook accepted without authenticity controls.
- API trusts client-supplied protected fields.
- Configurable destination routes sensitive data or credentialed backend requests to unapproved locations.
- Sensitive API/integration lacks meaningful resource limits where bulk exposure or operational harm is likely.

Orange:

- Authorization, authentication, webhook validation, destination allowlisting, service identity, response shaping, scopes, inventory, rate limits, provider behavior, or integration ownership incomplete for sensitive APIs/integrations.
- API key/token type or publishability unknown.
- Third-party responses/events trusted directly with unclear validation/authorization.

Yellow:

- API documentation, inventory, versioning, deprecation, schema, limit, logging, or error hygiene gap with low-risk scope.
- Approved integration needs documentation or least-privilege improvement.

Green:

- Public-by-design API with controls confirmed.
- Least-privilege authenticated/authorized API with response shaping and auditability.
- Signed/validated webhooks with replay/freshness controls.
- Approved integration with scoped credentials, safe logging, retention, owner, and revocation.
- Resource limits and monitoring match sensitivity/cost.

Gray:

- Endpoint, route, connector, webhook, callback, scope, credential, service identity, destination, data sensitivity, inventory status, or rate limit exists but effective control unknown.

Required evidence: Authn/authz, scopes, data/action classification, response shaping, schema validation, webhook controls, destination allowlist, rate limits, logging, integration owner, revocation, and current vendor/API docs.

Pass/fail: Fail on unauthorized API data/action exposure, live credential exposure, unverified sensitive webhooks, unapproved sensitive integrations, or unresolved sensitive API boundary unknowns.

## 07. Client-Side, Browser, and Frontend Exposure

Owns: Browser-visible code, frontend state, public assets, hydration data, source maps, storage, cookies, headers, scripts, tag managers, analytics, widgets, service workers, browser APIs, client routing/feature flags, DevTools-visible data, browser automation, and frontend trust assumptions.

Review focus: Is the client treated as untrusted, with no secrets, sensitive data, privileged logic, or security-critical decisions relying only on browser-side code, storage, scripts, or UI behavior?

Red:

- Secret, privileged credential, session material, or server-side secret in browser-visible context.
- Sensitive data delivered beyond expected authorized audience.
- Frontend-only controls are the only enforcement for privileged, paid, tenant, approval, admin, financial, or sensitive actions/data.
- Browser-controlled critical value accepted by backend.
- Sensitive session material, long-lived token, private data, or sensitive identifier exposed through unsafe storage, URLs, referrers, logs, caches, or service-worker caches.
- Unapproved third-party script, tag, replay, heatmap, chat, pixel, or widget captures sensitive data or runs on sensitive pages without controls.
- Public production source maps, build artifacts, or debug output expose secrets, sensitive data, privileged internals, or proprietary security-relevant code.

Orange:

- Visible key claimed publishable without restrictions confirmed.
- Sensitive browser data audience/minimization unknown.
- Backend enforcement behind hidden UI/client-side flags unknown.
- Cookie/storage/cache/referrer policy unknown for sensitive material.
- Third-party script masking/retention/approval unclear.
- Source map/debug artifact contents/access unclear.

Yellow:

- Minor browser header, cookie, referrer, source map, analytics, or frontend logging hygiene issue without sensitive impact.
- Non-sensitive public frontend config lacks documentation.

Green:

- Documented publishable/public key restricted and unable to access private data or privileged operations.
- Browser-visible data expected for current authorized user and minimized.
- Frontend controls are UX-only with backend enforcement confirmed.
- Non-sensitive preferences/UI state in storage.
- Approved scripts with masking, exclusions, retention, and governance.
- Restricted source maps or isolated non-production artifacts.

Gray:

- Value, data, storage, cookie, header, third-party script, source map, browser policy, or backend enforcement context unknown.

Required evidence: Browser-visible values, data category, backend enforcement, storage/cookie/header/cache/referrer posture, third-party script scope, source-map exposure, and current browser/vendor behavior.

Pass/fail: Fail when secrets, sessions, sensitive data, critical authorization, or financial decisions are exposed to or enforced only by the browser, or sensitive browser exposure remains unknown.
