# 13. Runtime, Memory, and Program Safety

Category ID: 13

Category name: Runtime, Memory, and Program Safety

## Purpose

Review whether runtime behavior, memory handling, unsafe code, parsers, plugins, workers, local tools, concurrency, sandboxing, and process permissions fail safely and stay within intended boundaries.

## Core Review Question

Are runtime behavior, memory handling, unsafe code, parsers, plugins, workers, local tools, concurrency, sandboxing, and process permissions designed to fail safely and stay within intended boundaries?

## Scope

Native/unsafe code, FFI/native modules/extensions, parsers, previews, converters, extractors, workers, queues, batch jobs, CLIs, scripts, plugins, macros, embedded interpreters, dynamic modules, crash/error/cleanup/rollback/fail-open behavior, process privileges, temp files, env vars, sandboxing, resource limits, concurrency, transactions, runtime dependencies, AI-generated/copied/vendor scripts and agents.

## Review Signals

- Untrusted files, messages, jobs, scripts, plugins, extensions, macros, AI-generated code, or vendor tools run with sensitive access.
- Parser/converter/preview/extraction behavior handles untrusted content.
- Runtime failure may fail open or expose diagnostics.
- Resource limits, isolation, temp-file handling, process privileges, dependency risk, or concurrency controls are unclear.

## Red Conditions

- Privileged untrusted unsafe/native execution.
- Privileged untrusted parsing, previewing, conversion, or extraction.
- Runtime failure fails open for security-relevant behavior.
- Sensitive diagnostic artifact exposure.
- Unreviewed executable content with sensitive access.
- Bypassing protective controls to run code, tools, files, or extensions.
- Untrusted privileged runtime extension.
- Privileged worker trusts untrusted jobs/messages.
- Reachable unmitigated high-risk native/parser/runtime dependency.
- Unbounded runtime resource use with serious impact.

## Orange Conditions

- Unsafe/native reachability, parser safety, diagnostic exposure, worker trust/privilege, runtime extension permissions, isolation coverage, vulnerable native/parser dependency reachability, AI/automation execution boundary, security-relevant concurrency, or vendor/local tool data handling requires owner confirmation.

## Yellow Conditions

- Limited hardening, testing, temp-file, resource-control, or concurrency gap.
- Safe low-impact crash/runtime error documentation gap.
- Approved runtime extension documentation gap.
- Non-reachable/low-risk dependency hygiene issue.
- Reviewed script or automation needs operational hardening.

## Green Conditions

- Memory-safe untrusted-input path.
- Controlled unsafe/native component.
- Controlled parser/converter worker.
- Controlled diagnostic handling.
- Safe runtime failure behavior.
- Controlled worker/script/batch execution.
- Approved scoped runtime extension/tool.
- Reviewed safe AI-generated/copied/local script execution.

## Gray Conditions

- Native code reachability, parser controls, crash impact, diagnostic controls, script/tool access, runtime extension trust, native/parser dependency risk, or control coverage unknown.

## Required Evidence

- Runtime path.
- Privilege level.
- Isolation/sandboxing.
- Parser/converter inputs.
- Diagnostic contents.
- Worker/job trust.
- Resource limits.
- Concurrency behavior.
- Dependency current status.
- Script/tool review ownership.

## Owners

Developer, security owner, operations owner, device-management owner, DevOps/release owner, cloud/platform owner, vendor owner, and AI governance owner.

## Non-Dev Action Checks

Do not run unknown scripts, AI-generated code, macros, plugins, suspicious files, or vendor tools on work devices or production-connected environments with sensitive access. Use reviewed code, sandboxed environments, synthetic data, and least privilege.

## Unsafe Request Boundaries

Do not request weaponized files, crash dumps with sensitive data, exploit samples, unsafe scripts, or live testing against production. Use synthetic fixtures, sandboxed review, and redacted diagnostics.

## Safe Evidence Handling

Use redacted stack traces, sanitized crash summaries, dependency/version summaries, sandbox design, worker trust summaries, resource-limit summaries, and owner-confirmed script/tool review status.

## False-Positive Guardrails

Do not mark Green because code is "local", "vendor-provided", "AI-generated", "only a script", or "runs once". Confirm privilege, data access, isolation, review, and failure behavior.

## Under-Classification Guardrails

Treat untrusted parsers, converters, macros, plugins, scripts, self-hosted tools, workers, and native dependencies as Orange or Red when privilege, isolation, or reachability is unclear.

## Currentness Notes

Check current native/parser/runtime dependency advisories, vendor tool behavior, platform sandboxing behavior, and runtime guidance where material.

## Category Gate Rule

Fails on privileged untrusted execution/parsing, unsafe diagnostics, fail-open runtime behavior, bypassed protections, untrusted broad extensions, or unresolved runtime unknowns affecting sensitive assets.
