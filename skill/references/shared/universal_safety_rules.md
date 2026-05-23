# Universal Safety Rules

These rules apply to every review depth and both review modes.

## Authorized Scope

Review only owned, authorized, synthetic, local-only, redacted, public, or owner-confirmed evidence. If authorization or ownership is unclear, classify the review boundary as Gray or Orange and ask for safe scope confirmation.

## Evidence Minimization

Ask only for safe context:

- Data type
- Environment
- Intended audience
- Owner
- Approval status
- Access model
- Retention
- Scope
- Control summaries

Do not ask for raw values when a redacted summary, synthetic example, owner confirmation, configuration summary, or public documentation is enough.

## Universal Prohibitions

Do not request, reproduce, validate, decode, test, or preserve:

- Raw secrets, tokens, passwords, private keys, session cookies, authorization headers, recovery codes, or connection strings
- Raw PII, customer records, employee records, private messages, support tickets, CRM records, production exports, or sensitive logs
- Private URLs, signed URLs, reset links, magic links, private screenshots, private prompts, tool-call payloads, private file paths, or sensitive resource identifiers
- Live credentials, credential validation output, or unsafe proof of access
- Exploit payloads, bypass steps, unauthorized testing instructions, enumeration workflows, or unsafe production validation
- Legal, privacy, or compliance conclusions

## Unsafe Validation

Do not ask the user to test a token, open a signed link, access another user's data, scan a third-party target, replay a webhook, change identifiers, run unsafe scripts, or stress production systems. Use passive review, redacted configuration review, synthetic fixtures, local-only examples, owner-approved test plans, and safe summaries instead.

## Classification Integrity

Keep severity separate from confidence. Impact and certainty are different. A high-impact issue with low certainty is not Green; it is usually Orange or Gray.

Use Gray when evidence is insufficient. Gray must not pass when the unknown affects sensitive data, credentials, production systems, authentication, authorization, privileged actions, external sharing, cloud or platform exposure, AI or automation access, customer impact, or legal/privacy/compliance-sensitive areas.

Escalate sensitive unknowns. Name the owner and the specific confirmation needed. Do not invent facts, assume safe defaults, or treat missing critical context as safe.

## Safe Reporting

The report must not become the leak. Redact first, then classify. Preserve only the type, location, exposure surface, environment, data category, actor or audience, owner, known controls, unknowns, and required action.

## Safe Remediation

Give defensive direction only: restrict access, remove exposure, rotate or revoke where exposure is plausible, minimize data, use synthetic or redacted evidence, add trusted server-side controls, use approved tools, add logging, and document owner approval. Do not include exploit detail.

## Browser-Delivered Content

For browser-delivered files or pages, treat all client-side HTML, JavaScript, CSS, comments, metadata, hidden fields, configuration, embedded data, runtime state, and bundled local files as shared with anyone who can access the page.

Not visible in the UI is not a security boundary. If sensitive or internal data is present in browser-delivered content, classify it as exposed to the page audience and route it to the appropriate owner for removal, minimization, or approval.

## Dashboard And Access-Control Remediation

Access controls can reduce who sees sensitive dashboard data, but they do not make browser-visible secrets safe. Secrets, tokens, connection strings, signing keys, session material, and credential-like values must be removed from client-side files and moved to trusted server-side handling or managed secret storage.

For sensitive internal dashboards, prefer approved authentication and role-based access such as SSO/RBAC over simple password-only sharing. Password-only sharing may reduce casual access, but it is not enough for sensitive data, privileged actions, exports, or browser-visible secrets.
