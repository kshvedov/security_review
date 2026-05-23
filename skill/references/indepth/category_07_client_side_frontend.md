# 07. Client-Side, Browser, and Frontend Exposure

Category ID: 07

Category name: Client-Side, Browser, and Frontend Exposure

## Purpose

Review whether browser-visible code, frontend state, public assets, scripts, source maps, browser storage, cookies, headers, analytics, widgets, and frontend assumptions expose sensitive material or create unsafe trust boundaries.

## Core Review Question

Is the client treated as untrusted, with no secrets, sensitive data, privileged logic, or security-critical decisions relying only on browser-side code, storage, scripts, or UI behavior?

## Scope

Frontend bundles, HTML, public JS/CSS/config/env vars, hydration data, source maps, browser storage, cookies, caches/service workers, client routing, feature flags, API requests/responses, browser security headers, third-party scripts, tag managers, analytics, replay, chat/widgets, postMessage, iframes, WebSocket/WebRTC/browser APIs, no-code landing pages, browser automation, and extensions.

## Review Signals

- Secret-like value, private data, session material, or privileged config is browser-visible.
- Frontend-only checks appear to control paid, tenant, admin, financial, approval, or sensitive actions.
- Browser storage, URL, cache, referrer, third-party script, source map, analytics, or replay may expose sensitive data.
- Backend enforcement is not proven.

## Red Conditions

- Secret, privileged credential, session material, or server-side secret in browser-visible context.
- Sensitive data delivered beyond expected authorized audience.
- Frontend-only controls are the only enforcement for privileged, paid, tenant, approval, admin, financial, or sensitive actions/data.
- Browser-controlled critical value accepted by backend.
- Sensitive session material, long-lived token, private data, or sensitive identifier exposed through unsafe storage, URLs, referrers, logs, caches, or service-worker caches.
- Unapproved third-party script, tag, replay, heatmap, chat, pixel, or widget captures sensitive data or runs on sensitive pages without controls.
- Public production source maps, build artifacts, or debug output expose secrets, sensitive data, privileged internals, or proprietary security-relevant code.

## Orange Conditions

- Visible key claimed publishable without restrictions confirmed.
- Sensitive browser data audience/minimization unknown.
- Backend enforcement behind hidden UI/client-side flags unknown.
- Cookie/storage/cache/referrer policy unknown for sensitive material.
- Third-party script masking/retention/approval unclear.
- Source map/debug artifact contents/access unclear.

## Yellow Conditions

- Minor browser header, cookie, referrer, source map, analytics, or frontend logging hygiene issue without sensitive impact.
- Non-sensitive public frontend config lacks documentation.

## Green Conditions

- Documented publishable/public key restricted and unable to access private data or privileged operations.
- Browser-visible data expected for current authorized user and minimized.
- Frontend controls are UX-only with backend enforcement confirmed.
- Non-sensitive preferences/UI state in storage.
- Approved scripts with masking, exclusions, retention, and governance.
- Restricted source maps or isolated non-production artifacts.

## Gray Conditions

- Value, data, storage, cookie, header, third-party script, source map, browser policy, or backend enforcement context unknown.

## Required Evidence

- Browser-visible values.
- Data category.
- Backend enforcement.
- Storage/cookie/header/cache/referrer posture.
- Third-party script scope.
- Source-map exposure.
- Current browser/vendor behavior where material.

## Owners

Developer, frontend owner, security owner, privacy owner, data owner, vendor owner, product owner, and DevOps/release owner.

## Non-Dev Action Checks

Do not put secret keys or private data into landing pages, tag managers, public scripts, local storage screenshots, or DevTools evidence. Treat the browser as visible and user-controlled.

## Unsafe Request Boundaries

Do not ask for DevTools screenshots containing private values, live tokens, raw local/session storage, private API responses, or proof by accessing unauthorized data. Use redacted summaries and synthetic examples.

## Safe Evidence Handling

Use redacted snippets, public/non-sensitive config summaries, cookie/header setting summaries, script/vendor inventories, source-map access summaries, and owner confirmations.

## False-Positive Guardrails

Do not mark Green because a value is "in frontend so public", hidden behind UI, minified, hard to find, or protected by obscurity. Confirm publishability, restrictions, backend enforcement, and audience.

## Under-Classification Guardrails

Treat browser-visible keys, source maps, hydration data, client flags, third-party scripts, replay tools, and browser storage as Orange or Red when sensitive or privileged context is plausible.

## Currentness Notes

Check current browser, framework, tag manager, replay/analytics vendor, source map, cookie, header, and platform behavior when those facts determine risk.

## Category Gate Rule

Fails when secrets, sessions, sensitive data, critical authorization, or financial decisions are exposed to or enforced only by the browser, or sensitive browser exposure remains unknown.
