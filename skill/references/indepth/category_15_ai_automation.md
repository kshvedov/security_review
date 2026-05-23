# 15. AI, Automation, and Agentic-System Safety

Category ID: 15

Category name: AI, Automation, and Agentic-System Safety

## Purpose

Review whether AI assistants, agents, RAG systems, tool-calling workflows, generated artifacts, no-code/RPA automations, SaaS connectors, and automated actions are constrained by safe data boundaries, least-privilege permissions, human approval where needed, trustworthy context handling, safe tool access, output review, auditability, and clear ownership.

## Core Review Question

Are AI and automation systems constrained by safe data boundaries, least-privilege permissions, human approval where needed, trustworthy context handling, safe tool access, output review, auditability, and clear ownership?

## Scope

AI assistants, chatbots, copilots, agents, browser/computer-use, tool-calling, RAG/vector databases/retrieval indexes/knowledge bases, embeddings, prompts/context/memory/uploads/logging/evaluation data, AI-generated code/scripts/queries/formulas/reports/communications/decisions, no-code/RPA/CRM/email/ticketing/support/marketing/data pipeline/cloud/finance automations, SaaS connectors, OAuth/service accounts/API tokens/browser sessions, action/tool logs, retention, vendor settings, and workspace config.

## Review Signals

- Secrets, credentials, customer data, employee data, confidential source, private docs, prompts, screenshots, support tickets, or production data enter AI/automation context.
- AI/automation has broad connectors, write/export/delete/send/deploy actions, browser/computer-use access, CRM/email/cloud/source access, or production sessions.
- RAG/vector/source scoping or authorization does not match original source permissions.
- Generated code, queries, reports, decisions, or communications are treated as authoritative without review.
- Retention, memory, logging, auditability, human approval, revocation, or vendor settings are unclear.

## Red Conditions

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

## Orange Conditions

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

## Yellow Conditions

- Low-risk ownership/documentation gap.
- Non-sensitive prompt/template hygiene gap.
- Low-impact audit/logging improvement.
- Advisory output review documentation gap.
- Non-sensitive AI log retention gap.
- Mostly scoped connector with documentation gap.
- Low-risk public chatbot documentation gap.
- Meeting assistant documentation gap.

## Green Conditions

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

## Gray Conditions

- Data category, AI vendor settings, connector permissions/actions, RAG ACL/lifecycle, AI memory/retention contents, generated-output review, accountability controls, or policy/legal/privacy obligations unknown.

## Required Evidence

- Data category.
- Approved tool/workspace settings.
- Connector scopes/actions.
- RAG ACLs and source equivalence.
- Prompt/memory/log retention.
- Human-approval gates.
- Generated-output review.
- Auditability.
- Revocation.
- Current AI/LLM/vendor/platform guidance.

## Owners

AI governance owner, security owner, data owner, privacy owner, vendor owner, identity owner, developer, DevOps/release owner, product owner, and operations owner.

## Non-Dev Action Checks

Do not paste secrets, customer records, private docs, support tickets, source with secrets, or production screenshots into AI tools. Do not connect agents to CRM, email, cloud, source, or production with broad scopes or autonomous actions without approval, logging, and revocation.

## Unsafe Request Boundaries

Do not request raw prompts with sensitive records, raw tool-call payloads, tokens, private documents, screenshots, customer records, or live agent credentials. Do not provide prompt injection, bypass, or autonomous misuse instructions. Use redacted summaries, approved workspace settings, synthetic data, and owner-confirmed scopes.

## Safe Evidence Handling

Use redacted prompt summaries, connector scope summaries, approved tool settings, retention/logging summaries, RAG/source ACL summaries, generated-artifact review status, and current official AI/vendor/platform guidance.

## False-Positive Guardrails

Do not mark Green because a tool is "enterprise", "encrypted", "approved", "read-only", "only a meeting assistant", or "the AI is secure" without confirming workspace settings, data category, retention, scopes, audit, and approval gates.

## Under-Classification Guardrails

Treat shadow AI, broad connectors, RAG sources, browser/computer-use sessions, hidden tool metadata, generated production artifacts, and autonomous actions as Orange or Red until controls are confirmed.

## Currentness Notes

Check current AI/LLM/vendor/platform guidance, workspace settings, retention/data-use terms, connector behavior, agent/tool-calling behavior, RAG/source authorization behavior, and emerging AI risks where material.

## Category Gate Rule

Fails on secrets/sensitive data in AI, cross-boundary retrieval leakage, autonomous high-impact actions without approval, unsafe sessions/credentials, unreviewed high-impact generated artifacts, or unresolved sensitive AI/automation unknowns.
