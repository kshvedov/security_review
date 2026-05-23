# 06. API, Service, and Integration Boundaries

Category ID: 06

Category name: API, Service, and Integration Boundaries

## Purpose

Review whether APIs, backend services, webhooks, callbacks, partner connections, no-code integrations, automation connectors, service identities, schemas, scopes, limits, logs, and vendor integrations are safe to expose, call, trust, consume, or connect for the data and actions they handle.

## Core Review Question

Is the API, service, webhook, callback, connector, automation, or integration boundary safe to expose, call, trust, consume, or connect for the data and actions it handles?

## Scope

APIs, backend services, internal/external services, webhooks, callbacks, partner connections, no-code integrations, automation connectors, machine-to-machine workflows, OAuth scopes, service accounts, schemas, response shaping, limits, errors, logs, inventory, and vendor integrations.

## Review Signals

- API route, webhook, callback, connector, service account, or vendor integration handles sensitive data or privileged actions.
- Response includes more fields than the caller needs.
- Scopes are broad, unclear, long-lived, or ownerless.
- External events or third-party responses are trusted without clear validation.
- Resource limits, logging, revocation, or integration ownership is unclear.

## Red Conditions

- Unauthorized sensitive API data exposure.
- Privileged API action exposed without confirmed server-side authorization.
- Live API/integration credential exposed.
- Restricted/private/admin/debug/staging/internal/deprecated API publicly reachable with sensitive impact.
- Unapproved third-party/no-code/automation/AI access to sensitive production APIs.
- Sensitive webhook accepted without authenticity controls.
- API trusts client-supplied protected fields.
- Configurable destination routes sensitive data or credentialed backend requests to unapproved locations.
- Sensitive API/integration lacks meaningful resource limits where bulk exposure or operational harm is likely.

## Orange Conditions

- Authorization, authentication, webhook validation, destination allowlisting, service identity, response shaping, scopes, inventory, rate limits, provider behavior, or integration ownership incomplete for sensitive APIs/integrations.
- API key/token type or publishability unknown.
- Third-party responses/events trusted directly with unclear validation or authorization.

## Yellow Conditions

- API documentation, inventory, versioning, deprecation, schema, limit, logging, or error hygiene gap with low-risk scope.
- Approved integration needs documentation or least-privilege improvement.

## Green Conditions

- Public-by-design API with controls confirmed.
- Least-privilege authenticated/authorized API with response shaping and auditability.
- Signed/validated webhooks with replay/freshness controls.
- Approved integration with scoped credentials, safe logging, retention, owner, and revocation.
- Resource limits and monitoring match sensitivity/cost.

## Gray Conditions

- Endpoint, route, connector, webhook, callback, scope, credential, service identity, destination, data sensitivity, inventory status, or rate limit exists but effective control unknown.

## Required Evidence

- Authn/authz.
- Scopes.
- Data/action classification.
- Response shaping.
- Schema validation.
- Webhook controls.
- Destination allowlist.
- Rate limits.
- Logging.
- Integration owner.
- Revocation.
- Current vendor/API docs.

## Owners

Developer, API owner, security owner, vendor owner, identity owner, data owner, privacy owner, AI governance owner, and operations owner.

## Non-Dev Action Checks

Do not grant broad API scopes, paste tokens, publish private docs/logs/responses, or connect tools without owner approval. Ask what data/actions the integration can read, write, export, delete, how it is logged, and how it is revoked.

## Unsafe Request Boundaries

Do not request tokens, raw responses with sensitive data, live endpoint probing, unauthorized enumeration, replaying webhooks, or proof of access. Use redacted summaries, schemas, scope lists, and owner-confirmed settings.

## Safe Evidence Handling

Use redacted API summaries, schema snippets without sensitive values, scope/permission summaries, architecture descriptions, safe logs, owner confirmations, and current provider docs.

## False-Positive Guardrails

Do not mark Green because an API is "internal", a webhook is "secret", an integration is "approved", or scopes are "read-only" without verifying data, actions, audience, retention, logs, and revocation.

## Under-Classification Guardrails

Treat broad scopes, configurable destinations, webhooks, partner APIs, deprecated endpoints, internal/admin routes, and AI/no-code connectors as Orange or Gray until controls and ownership are confirmed.

## Currentness Notes

Check current API/vendor docs for scope behavior, webhook validation, retention, connector behavior, provider defaults, rate limits, and deprecation/security advisories where material.

## Category Gate Rule

Fails on confirmed unauthorized API data/action exposure, live credential exposure, unverified sensitive webhooks, unapproved sensitive integrations, or unresolved sensitive API boundary unknowns.
