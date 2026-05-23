# 05. Input, Query, and Execution Safety

Category ID: 05

Category name: Input, Query, and Execution Safety

## Purpose

Review whether untrusted, external, file-derived, AI-generated, user-controlled, or workflow-provided input is safely handled before it affects queries, execution, rendering, routing, paths, commands, templates, redirects, backend requests, parsers, or trusted behavior.

## Core Review Question

Are untrusted inputs validated, constrained, encoded, parameterized, escaped, parsed, and handled before they affect queries, execution, rendering, paths, destinations, or sensitive backend behavior?

## Scope

Queries, database filters, search, commands, subprocesses, scripts, eval-like behavior, template rendering, file/object paths, redirects, callbacks, server-side requests, webhook payloads, file parsers, deserializers, generated code, generated formulas, no-code workflows, AI-generated outputs, and sensitive logs derived from input.

## Review Signals

- User, file, webhook, vendor, AI, no-code, or external workflow input controls structure, destination, path, template, command, query, or execution behavior.
- Generated code/query/script/formula is used against sensitive or production systems.
- Webhook or external event triggers privileged logic.
- Input-derived values appear in logs, screenshots, or downstream artifacts that may contain sensitive data.

## Red Conditions

- Untrusted input directly controls production/sensitive query logic without confirmed parameterization or allowlisted structure.
- Input controls command, shell, subprocess, or script execution without strict controls.
- Input reaches eval-like execution or dynamic loading without isolation.
- Unsafe deserialization/parser behavior in production or sensitive context.
- Input-controlled backend request destination crosses internal, cloud, or privileged boundaries.
- Input-controlled file/object/include/template path reaches sensitive resources.
- Input-controlled redirect/callback creates sensitive workflow risk.
- Untrusted rendered content becomes active content in sensitive user/admin context.
- Unverified webhook or external payload triggers privileged logic.
- AI/no-code/generated output acts on production/sensitive systems without review.

## Orange Conditions

- Source/sink/control status incomplete for sensitive query, command, template, path, destination, parser, webhook, AI/no-code, or automation flow.
- Client/workflow controls structural fields, operators, or destinations but mapping is unclear.
- Generated code/query/script/formula review unknown.
- Logs/screenshots may contain sensitive input-derived values.

## Yellow Conditions

- Low-risk validation, documentation, sanitizer policy, schema, parser setting, redirect mapping, or review-process gap with no sensitive or production impact.
- Controlled generated output needs ticketed review documentation.
- Minor redaction cleanup.

## Green Conditions

- Values parameterized and structural parts server-side allowlisted.
- Output encoded/sanitized for exact context.
- Commands use fixed operations with separated allowlisted arguments and least privilege.
- Destinations/paths server-generated or allowlisted with boundary checks.
- Webhooks verified, schema-validated, freshness/replay-controlled, and least-privilege mapped.
- Generated outputs are advisory or owner-reviewed before use.

## Gray Conditions

- Input source, sink, environment, sensitivity, structural control, sanitizer policy, parser setting, webhook verification, or generated-output review unknown.

## Required Evidence

- Input source and sink.
- Data/control separation.
- Validation and allowlist behavior.
- Encoding or parameterization.
- Parser/deserialization controls.
- Privilege boundary.
- Generated-output review status.
- Current framework/library behavior where relevant.

## Owners

Developer, security owner, operations owner, data owner, product owner, vendor owner, AI governance owner, and device-management owner.

## Non-Dev Action Checks

Do not run generated scripts, queries, formulas, macros, or no-code workflows against production or sensitive systems without developer/security review. Do not paste raw records. Use reviewed templates, approved workflows, and synthetic data.

## Unsafe Request Boundaries

Do not provide exploit strings, bypass examples, or live test instructions. Do not ask the user to run unsafe scripts, stress production, replay webhooks, or validate against data they do not own. Use safe design review and synthetic fixtures.

## Safe Evidence Handling

Use redacted snippets, pseudocode summaries, architecture diagrams, synthetic input/output examples, schema summaries, and owner-confirmed controls. Avoid raw payloads, raw records, production logs, or unsafe validation output.

## False-Positive Guardrails

Do not mark Green just because a framework "usually handles it", input is "internal", or a tool generated the query. Confirm exact sink behavior and whether structure can be influenced.

## Under-Classification Guardrails

Treat structural query fields, destinations, paths, templates, commands, callbacks, webhooks, and generated outputs as risky until source/sink/control mapping is clear.

## Currentness Notes

Check current framework, parser, dependency, webhook provider, browser, and AI/no-code platform behavior when it affects sink safety or mitigation.

## Category Gate Rule

Fails on confirmed untrusted input reaching high-risk sinks without controls or unresolved input-safety unknowns affecting sensitive data, production systems, privileged actions, or external sharing.
