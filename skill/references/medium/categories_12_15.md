# Medium Categories 12-15

Use this file with `medium_review.md`, `category_router.md`, and the shared references. Category detail here is stronger than Quick and less exhaustive than Indepth.

## 12. Cryptography, Transport, and Data Protection Controls

Owns: TLS/HTTPS/HSTS/mixed content/certificates/mTLS, encryption at rest/field/envelope/database/storage/backup/log/file/export, password hashing/KDFs/salts, randomness/nonces/IVs/tokens/reset links/session IDs, JWT/message/webhook signing, KMS/key vault/HSM/key lifecycle/separation/rotation/revocation/access, masking/tokenization/pseudonymization/anonymization/deletion, vendor/SaaS/AI encryption claims.

Review focus: Are encryption, hashing, signing, transport security, certificate validation, random generation, password protection, and data-protection controls appropriate for the data, system, environment, and threat model?

Red:

- Sensitive data/credentials sent over unprotected transport.
- Certificate validation disabled or trust-any behavior in production/sensitive use.
- Plaintext, reversible, unsalted, or fast-hashed passwords for real users.
- Private/signing/encryption keys or production crypto material exposed or shared unsafely.
- Missing or fail-open signing/integrity verification for sensitive trust-boundary messages.
- Production crypto keys reused in test, demo, local, AI, vendor, or uncontrolled workflows.
- Unreviewed custom or AI-generated cryptography protects real sensitive assets.
- Sensitive backups, exports, logs, or files unencrypted or weakly protected in unsafe sharing/storage.
- Predictable security tokens, reset links, session IDs, nonces, IVs, or salts affect real security decisions.

Orange:

- Transport protection incomplete or uncertain.
- Invalid, self-signed, or unmanaged certificate in sensitive context.
- Weak/deprecated TLS, cipher, algorithm, library, or parameter suspected.
- Password hashing parameters unknown or weak.
- Token/JWT/webhook/message validation incomplete.
- Encryption at rest exists but decrypt access, key ownership, or field-level need unknown.
- Vendor/SaaS/AI encryption claim insufficient.
- Key lifecycle, rotation, revocation, access, or separation unclear.
- Client-side/E2E trust model unclear.
- Custom/AI crypto deployment or review unknown.
- Masking, tokenization, anonymization, or deletion claims need owner review.
- Current vulnerability/platform/vendor behavior may affect risk.

Yellow:

- Certificate renewal, monitoring, ownership, or inventory gap.
- Low-risk HTTPS/HSTS/redirect/mixed-content hygiene issue.
- Approved encryption/KMS/key vault/HSM/managed TLS lacks documentation.
- Password hashing tuning or migration contained.
- Publishable key restriction documentation gap.
- Crypto library/TLS/cert automation/platform update needs ticketing.
- Secure-transfer process needs ownership.
- Source freshness re-check needed before live advice.

Green:

- HTTPS/TLS enforced and transport path documented.
- Self-signed/private-CA cert limited to controlled internal/local/test trust context.
- Managed TLS, encryption, KMS, key vault, HSM, service mesh, or cloud control matches data risk.
- Approved password hashing with appropriate salts/parameters.
- Token/JWT/message/webhook verification uses approved libraries and fails closed.
- Visible key/client ID documented publishable and restricted.
- Synthetic/local examples only.
- Standard crypto libraries and approved key management used.
- External sharing uses approved secure transfer and data-governance controls.

Gray:

- HTTPS redirect/mixed content/backend transport, cert validation/trust model, hash purpose/security role, signing validation, decrypt access, vendor encryption access/retention/key-management/approval context, client-side/E2E trust model, key lifecycle/secure deletion, or randomness/nonce/IV/reset-link/token/salt source unknown.

Required evidence: Data sensitivity, transport path, certificate validation, algorithm/library/version/current guidance, password hashing parameters, key ownership/storage/rotation/access, verification failure behavior, secure deletion scope, and vendor/platform current docs.

Pass/fail: Fail on unprotected sensitive transport, disabled cert validation in sensitive use, unsafe password/crypto/key handling, missing verification at trust boundaries, or unresolved crypto context for sensitive assets.

## 13. Runtime, Memory, and Program Safety

Owns: Native/unsafe code, FFI/native modules/extensions, parsers, previews, converters, extractors, workers, queues, batch jobs, CLIs, scripts, plugins, macros, embedded interpreters, dynamic modules, crash/error/cleanup/rollback/fail-open behavior, process privileges, temp files, env vars, sandboxing, resource limits, concurrency, transactions, runtime dependencies, AI-generated/copied/vendor scripts and agents.

Review focus: Are runtime behavior, memory handling, unsafe code, parsers, plugins, workers, local tools, concurrency, sandboxing, and process permissions designed to fail safely and stay within intended boundaries?

Red:

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

Orange:

- Unsafe/native reachability, parser safety, diagnostic exposure, worker trust/privilege, runtime extension permissions, isolation coverage, vulnerable native/parser dependency reachability, AI/automation execution boundary, security-relevant concurrency, or vendor/local tool data handling requires owner confirmation.

Yellow:

- Limited hardening, testing, temp-file, resource-control, or concurrency gap.
- Safe low-impact crash/runtime error documentation gap.
- Approved runtime extension documentation gap.
- Non-reachable/low-risk dependency hygiene issue.
- Reviewed script or automation needs operational hardening.

Green:

- Memory-safe untrusted-input path.
- Controlled unsafe/native component.
- Controlled parser/converter worker.
- Controlled diagnostic handling.
- Safe runtime failure behavior.
- Controlled worker/script/batch execution.
- Approved scoped runtime extension/tool.
- Reviewed safe AI-generated/copied/local script execution.

Gray:

- Native code reachability, parser controls, crash impact, diagnostic controls, script/tool access, runtime extension trust, native/parser dependency risk, or control coverage unknown.

Required evidence: Runtime path, privilege level, isolation/sandboxing, parser/converter inputs, diagnostic contents, worker/job trust, resource limits, concurrency behavior, dependency current status, and script/tool review ownership.

Pass/fail: Fail on privileged untrusted execution/parsing, unsafe diagnostics, fail-open runtime behavior, bypassed protections, untrusted broad extensions, or unresolved runtime unknowns affecting sensitive assets.

## 14. Logging, Monitoring, Auditability, and Incident Readiness

Owns: Application/API/auth/admin/identity/cloud/IAM/database/storage/CI/CD/SaaS/vendor/support/no-code/AI/automation/webhook/service logs, dashboards, SIEM/SOC alerts, runbooks, incident records, retention/access/log integrity/redaction/masking, and audit coverage for high-risk actions.

Review focus: Can the right people detect, understand, attribute, preserve safe evidence, and respond to suspicious, abusive, unauthorized, privacy-impacting, or operationally unsafe events without exposing secrets or private data?

Red:

- Live secret/credential in logs or incident evidence.
- Raw sensitive personal/customer/employee/production data exposed through logs.
- Public/broad sensitive logs, dashboards, traces, or incident evidence.
- Sensitive/privileged production actions unauditable.
- Audit logs alterable, deletable, or disableable by audited actors.
- Shared/generic privileged account makes high-risk actions unattributable.
- High-risk alerts intentionally disabled, ignored, or ownerless.
- Unsafe non-dev action creates serious audit/evidence exposure failure.

Orange:

- Sensitive action logging may be missing.
- Logs may contain secrets or credentials but type/exposure unclear.
- Logs may contain PII/private records but sensitivity/approval unclear.
- Alert owner, routing, triage, or response unclear.
- Cloud/identity/SaaS/vendor audit coverage unconfirmed.
- Retention, access, redaction, or provider behavior uncertain.
- AI/automation action logging or prompt/tool-log handling unclear.
- External log sharing lacks approval, redaction, or retention confirmation.

Yellow:

- Low-risk logging coverage gap.
- Documentation missing for functioning controls.
- Alert tuning issue for lower-risk owner-monitored events.
- Non-sensitive debug logging cleanup or time limit.
- Event schema improvement.
- Retention rationale/review cadence.
- Runbook/escalation refinement.

Green:

- Security events logged with safe metadata and no sensitive payloads.
- Privacy-preserving minimal logging supports investigations.
- Managed provider logging coverage, retention, and export verified.
- Actionable owner-routed alerts with runbooks.
- Log access, retention, and integrity controls protect evidence.
- Privileged/vendor/support actions attributable to named actors.
- AI/automation tool-call logs capture safe metadata, approvals, and outcomes.

Gray:

- Audit coverage, log contents, credential-like value, alert ownership, retention, provider behavior, shared/automation attribution, or incident readiness unknown.

Required evidence: Event coverage, safe fields logged, redaction/masking, access controls, retention, alert owner/routing, integrity controls, runbooks, provider/vendor current docs, and attribution for privileged/AI/automation actions.

Pass/fail: Fail on secrets/PII in logs, broad sensitive dashboard exposure, unauditable high-risk actions, log tampering risk, disabled high-risk alerts, or unresolved auditability unknowns for sensitive areas.

## 15. AI, Automation, and Agentic-System Safety

Owns: AI assistants, chatbots, copilots, agents, browser/computer-use, tool-calling, RAG/vector databases/retrieval indexes/knowledge bases, embeddings, prompts/context/memory/uploads/logging/evaluation data, AI-generated code/scripts/queries/formulas/reports/communications/decisions, no-code/RPA/CRM/email/ticketing/support/marketing/data pipeline/cloud/finance automations, SaaS connectors, OAuth/service accounts/API tokens/browser sessions, action/tool logs, retention, vendor settings, and workspace config.

Review focus: Are AI and automation systems constrained by safe data boundaries, least-privilege permissions, human approval where needed, trustworthy context handling, safe tool access, output review, auditability, and clear ownership?

Red:

- Real secrets/credentials in AI/automation context.
- Unapproved real sensitive data sent to AI/vendor tools.
- Cross-boundary AI context/retrieval leakage.
- High-impact autonomous actions without meaningful approval.
- Unsafe credentials or sessions for privileged AI/automation work.
- Unreviewed AI-generated production artifact with high impact.
- Authoritative AI output in high-impact decisions without review.
- Unrestricted external data transfer by AI/automation.
- Public AI interface exposes internal/sensitive information.
- Unrevoked high-impact AI/automation access.

Orange:

- Sensitive AI data handling unknown.
- Broad or unclear connector permissions.
- Agent actions with unclear approval boundaries.
- RAG authorization or scoping unknown.
- Sensitive AI retention, memory, or logging unknown.
- Browser/computer-use production session risk.
- AI-generated artifact review status unknown.
- Sensitive model-output trust unknown.
- Public chatbot controls unknown.
- Vendor claims not environment-confirmed.
- Sensitive hidden instructions/tool metadata.
- Shadow/personal AI use with unknown data sensitivity.

Yellow:

- Low-risk ownership/documentation gap.
- Non-sensitive prompt/template hygiene gap.
- Low-impact audit/logging improvement.
- Advisory output review documentation gap.
- Non-sensitive AI log retention gap.
- Mostly scoped connector with documentation gap.
- Low-risk public chatbot documentation gap.
- Meeting assistant documentation gap.

Green:

- Safe data category confirmed.
- Advisory-only low-risk output.
- Reviewed generated artifact.
- Approved read-only least-privilege assistant.
- Source-equivalent RAG authorization.
- Confirmed approved enterprise AI settings.
- Enforced human approval for sensitive actions.
- Safe automation identity.
- Safe scoped public chatbot.
- Controlled AI meeting assistant.

Gray:

- Data category, AI vendor settings, connector permissions/actions, RAG ACL/lifecycle, AI memory/retention contents, generated-output review, accountability controls, or policy/legal/privacy obligations unknown.

Required evidence: Data category, approved tool/workspace settings, connector scopes/actions, RAG ACLs and source equivalence, prompt/memory/log retention, human-approval gates, generated-output review, auditability, revocation, and current AI/LLM/vendor/platform guidance.

Pass/fail: Fail on secrets/sensitive data in AI, cross-boundary retrieval leakage, autonomous high-impact actions without approval, unsafe sessions/credentials, unreviewed high-impact generated artifacts, or unresolved sensitive AI/automation unknowns.
