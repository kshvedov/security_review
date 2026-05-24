# Security Review Help

Use this skill when you want a security review or a safe action check.

Invoke it manually with `/security_review` or `$security-review`.

## Basic Prompt

```text
/security_review

Analysis depth: Quick
Output type: non-technical

Question:
Can I paste this redacted customer issue summary into an AI chat to make it clearer?
```

## Depth Levels

- Quick: short triage, top risks, immediate next step.
- Medium: normal review with grouped issue families, remediation, and owner routing.
- Indepth: comprehensive review for deeper or final-gate decisions.

## Output Types

- non-technical: plain-language risk and action guidance.
- technical: more implementation detail and security terminology.

## Good Questions

```text
/security_review

Analysis depth: Quick
Output type: non-technical

Question:
Can I send these raw logs to a vendor for debugging?
```

```text
/security_review

Analysis depth: Medium
Output type: non-technical

Question:
I want to share this HTML dashboard with the whole company. Is it safe, and what should I fix first?
```

```text
$security-review

Analysis depth: Medium
Output type: technical

Question:
Review this configuration before we deploy it.
```

```text
/security_review

Analysis depth: Indepth
Output type: technical

Question:
Review this AI invoice assistant design before approval.
```

## Safe Input

Do not paste raw secrets, passwords, tokens, private keys, customer records, private screenshots, private URLs, raw logs, or live credential test results.

Use redacted snippets, synthetic examples, safe summaries, intended audience, owner, approval status, access model, retention, and relevant configuration summaries.
