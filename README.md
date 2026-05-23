# Security Review

Security review skill for AI-assisted code, data, vendor, browser, and non-developer safety checks, with structured risk classification and expectation-based evals.

Short description:

```text
Structured security review skill for AI-created code, data exposure, browser content, vendors, and non-developer safety checks.
```

## Purpose

This repo contains a final Security Review Skill and a lean eval set for checking that the skill keeps its safety behavior over time.

The skill is intended to help with:

- AI-created code and configuration review
- Accidental data exposure checks
- Secrets, credentials, logs, screenshots, files, and browser-delivered content
- Vendor, AI tool, and non-developer action-safety questions
- Structured Red, Orange, Yellow, Green, and Gray risk classification

This is not a penetration-testing or exploitation skill. It is a review barrier that classifies risk, preserves redaction, asks only for safe context, and provides defensive remediation.

## Layout

```text
security_review/
  skill/
    SKILL.md
    references/
  evals/
    prompts/
    fixtures/
    expected_checks.md
```

- `skill/` is the installable skill package.
- `evals/prompts/` contains reusable prompt inputs.
- `evals/fixtures/` contains sanitized local fixtures.
- `evals/expected_checks.md` defines behavior expectations instead of exact golden answers.

Generated model responses should be saved outside the repo or under ignored paths such as `evals/results/`.

## Use

In a new chat or review session, start with:

```text
Read `skill/SKILL.md`

Analysis depth: Quick / Medium / Indepth
Output type: technical / non-technical

Question:
<your security review question>
```

Depth controls detail only. It must not change the required audit format, classification model, redaction rules, pass/fail logic, or safety boundaries.

## Evals

To run an eval manually:

1. Open one prompt from `evals/prompts/`.
2. Paste it into a fresh chat or review session.
3. Compare the result to `evals/expected_checks.md`.
4. Save temporary outputs under `evals/results/` if needed. That path is ignored by git.

Do not rely on exact response text. Judge whether the result satisfies the required format and behavior checks.

## Safety Boundaries

- Do not request, paste, preserve, validate, decode, or test live secrets.
- Do not reproduce raw PII, private screenshots, private URLs, raw logs, customer records, private messages, session cookies, tokens, passwords, private keys, or connection strings.
- Redact sensitive values and describe only type, location, exposure surface, environment if known, data category, owner, and required action.
- Do not include exploit payloads, bypass steps, unauthorized testing instructions, or credential-use instructions.
- Do not provide legal conclusions. Escalate legal, privacy, and compliance-sensitive questions to the proper owner.
