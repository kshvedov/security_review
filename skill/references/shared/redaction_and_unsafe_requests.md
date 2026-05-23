# Redaction And Unsafe Requests

Redact first, then classify. The review output must preserve useful security context without exposing sensitive values.

## Evidence Separation

Keep these separate in every review:

- Observed evidence: What was directly seen or provided after redaction.
- Current-source verification: What current authoritative sources or owner-confirmed current context were checked, or what could not be verified.
- Inferred risk: What the evidence suggests could happen.
- Assumptions: What is being assumed but not proven.
- Unknowns: What is missing or unclear.
- Required confirmation: Who must confirm what.
- Redactions: What sensitive values were removed.
- Safer alternatives: How to proceed safely.
- Gate impact: Pass, fail, escalation, more context, ticketing, or acceptance.

## Safe Evidence

Safe evidence includes redacted screenshots, redacted logs, redacted configuration summaries, redacted API/request/response summaries, synthetic examples, local-only fixtures, public documentation, current vendor or platform documentation, owner-confirmed settings, architecture descriptions, permission summaries, data-flow descriptions, workflow descriptions, and scan summaries with sensitive values removed.

## Unsafe Evidence

Unsafe evidence includes raw API keys, tokens, session cookies, passwords, private keys, raw PII, customer or employee records, private messages, production exports, live signed URLs, full authorization headers, private screenshots, logs with secrets or records, unauthorized validation output, and live access proof for data the user does not own.

Do not request or repeat unsafe evidence. If it was already shared, do not reproduce it. State that it was redacted and recommend containment, owner review, rotation or revocation where plausible, and safer evidence handling.

## Placeholder Examples

Use placeholders that preserve category and context without exposing raw values:

| Sensitive item | Replacement wording |
|---|---|
| Raw secret | [REDACTED SECRET] |
| API key | [REDACTED API KEY] |
| Access token, bearer token, or JWT | [REDACTED ACCESS TOKEN] or [REDACTED TOKEN] |
| Refresh token | [REDACTED REFRESH TOKEN] |
| Session cookie or session ID | [REDACTED SESSION COOKIE] or [REDACTED SESSION ID] |
| Authorization header | [REDACTED AUTHORIZATION HEADER] |
| Password or temporary password | [REDACTED PASSWORD] |
| MFA, recovery, or backup code | [REDACTED MFA OR RECOVERY CODE] |
| Private, signing, or encryption key | [REDACTED PRIVATE KEY], [REDACTED SIGNING KEY], or [REDACTED ENCRYPTION KEY] |
| Connection string | [REDACTED CONNECTION STRING] |
| Cloud, service account, CI/CD, or registry credential | [REDACTED CLOUD CREDENTIAL], [REDACTED SERVICE ACCOUNT KEY], [REDACTED CI/CD TOKEN], or [REDACTED REGISTRY TOKEN] |
| Webhook secret or signature header | [REDACTED WEBHOOK SECRET] or [REDACTED SIGNATURE HEADER] |
| OAuth or SAML artifact | [REDACTED OAUTH OR SAML ARTIFACT] |
| Private URL, signed URL, reset link, or magic link | [REDACTED PRIVATE URL], [REDACTED SIGNED URL], or [REDACTED RESET OR MAGIC LINK] |
| Customer contact detail | [REDACTED CUSTOMER EMAIL], [REDACTED CUSTOMER NAME], [REDACTED CUSTOMER PHONE], or [REDACTED ADDRESS] |
| Employee data | [REDACTED EMPLOYEE DATA] |
| Private message, support ticket, or CRM record | [REDACTED PRIVATE MESSAGE], [REDACTED SUPPORT TICKET CONTENT], or [REDACTED CRM RECORD] |
| Customer/account/tenant/user/object/file/order/invoice ID | [REDACTED ACCOUNT ID], [REDACTED TENANT ID], [REDACTED USER ID], or [REDACTED OBJECT ID] |
| API response, query result, database row, or CSV row | [REDACTED API RESPONSE BODY], [REDACTED QUERY RESULT], [REDACTED DATABASE ROW], or [REDACTED CSV ROW] |
| Log, stack trace, crash dump, or diagnostic bundle | [REDACTED LOG ENTRY], [REDACTED STACK TRACE], or [REDACTED DUMP CONTENTS] |
| Sensitive file path, object path, resource name, or internal host | [REDACTED FILE PATH], [REDACTED OBJECT PATH], [REDACTED RESOURCE NAME], or [REDACTED INTERNAL HOSTNAME] |
| Screenshot or dashboard | [REDACTED SCREENSHOT] or [REDACTED DASHBOARD SCREENSHOT] |
| AI prompt, output, memory, or tool call | [REDACTED SENSITIVE PROMPT CONTENT], [REDACTED AI OUTPUT], [REDACTED AI MEMORY CONTENT], or [REDACTED TOOL-CALL PAYLOAD] |
| Vendor or tool evidence | [REDACTED VENDOR OR TOOL EVIDENCE] |

If a file name, project name, route, resource name, hostname, path, tenant ID, or screenshot can reveal sensitive identity, infrastructure, customer, legal, health, financial, or confidential business information, redact it too.

## Unsafe Request Handling

| Unsafe request type | Why unsafe | Redirect safely |
|---|---|---|
| Exploit or payload request | Teaches offensive behavior. | Provide high-level risk explanation, safe detection criteria, and defensive remediation. |
| Bypass request | Helps defeat controls. | Explain that controls should be verified through authorized review and owner-approved synthetic fixtures. |
| Credential-use request | Could enable unauthorized access. | Refuse use or validation; ask for redacted type and location only; recommend owner-led rotation or revocation if exposed. |
| Secret-copying request | Expands blast radius. | Ask for placeholder and context only; never copy the raw value. |
| PII reproduction request | Creates privacy exposure. | Use category-level summaries and redacted placeholders. |
| Unauthorized testing request | May affect real systems or data without permission. | Require safe scope confirmation and suggest passive review, code/config review, or authorized test fixtures. |
| Enumeration request | Could expose real users, tenants, records, files, endpoints, or accounts. | Discuss inventory or access-control review at a high level using owner-approved summaries. |
| Unsafe production validation | Can harm customers, data, availability, or legal/privacy posture. | Use staging or synthetic fixtures, owner-approved change windows, and safe summaries. |
| Unsafe script or tool execution | Could leak data or damage systems. | Recommend review, sandboxing, least privilege, synthetic data, and owner approval. |
| Legal/compliance conclusion request | Requires qualified owner or legal interpretation. | Provide technical facts, risks, and owner questions; do not decide legality or compliance. |
