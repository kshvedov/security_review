# Security Review

Structured security review skill for AI-created code, data exposure, browser content, vendors, and non-developer safety checks.

This repo contains an installable AI skill plus a small expectation-based eval set. The skill is designed to act as a review barrier: it classifies risk, preserves redaction, asks for safe context only, and gives defensive next steps without teaching exploitation.

## What This Helps With

Use this skill when you want to know whether something is safe to share, deploy, paste into an AI tool, send to a vendor, publish, or use in a workflow.

Good fit:

- AI-created code, scripts, configuration, dashboards, or automations
- Secrets, tokens, keys, passwords, connection strings, and credential-like values
- Customer data, employee data, private logs, screenshots, exports, and files
- Browser-delivered HTML, JavaScript, hidden state, metadata, and bundled assets
- Vendor sharing, AI tool use, no-code workflows, permissions, integrations, and access review
- Non-developer questions like "Can I do this safely?" or "What should I fix first?"

Not a fit:

- Exploit development
- Bypass instructions
- Unauthorized testing
- Live credential validation
- Legal conclusions

## How To Use It

### Quick Install From Zip

If your AI tool supports importing a skill from a zip file, download `security_review.zip` from this repo and import it.

The zip contains the installable `skill/` package only. It does not include eval fixtures or generated responses.

After import, call the skill explicitly with `/security_review`.

If you edit the source files under `skill/`, regenerate `security_review.zip` before sharing it.

If the skill is installed in your AI tool, call it explicitly. This avoids accidental activation and avoids expensive deep reviews when you only wanted a normal answer.

Ask your question in this shape:

```text
/security_review

Analysis depth: Quick
Output type: non-technical

Question:
Can I paste this redacted customer issue summary into an AI chat to make it clearer?
```

For a short usage guide after installation, ask:

```text
/security_review help
```

or:

```text
security_review --help
```

If your AI tool does not support slash commands, you can also say:

```text
Use the security_review skill.

Analysis depth: Medium
Output type: technical

Question:
Review this configuration before we deploy it.
```

For local testing without installing the skill, use:

```text
Read `skill/SKILL.md`

Analysis depth: Quick
Output type: non-technical

Question:
<your security review question>
```

## Choose A Depth

Use one of these depth levels:

| Depth | Use when | Result style |
|---|---|---|
| Quick | You need fast triage or a simple action-safety answer. | Short decision, top risks, immediate next step. |
| Medium | You need a normal security review. | Grouped major issue families, remediation, owner routing. |
| Indepth | You need comprehensive review or final-gate confidence. | Broader issue-family coverage with representative evidence. |

Depth changes the amount of detail only. It does not change the required audit format, safety rules, classification logic, redaction handling, or pass/fail logic.

## Choose An Output Type

Use one of these output types:

| Output type | Use when |
|---|---|
| non-technical | You want plain-language risk and action guidance. |
| technical | You want more implementation detail and security terminology. |

The skill does not guess whether the user is technical. Say the output type you want.

## Example Questions

```text
Analysis depth: Quick
Output type: non-technical

Question:
Can I send these raw application logs to a vendor for debugging?
```

```text
Analysis depth: Medium
Output type: non-technical

Question:
I want to share this HTML dashboard with the whole company. Is it safe, and what should I fix first?
```

```text
Analysis depth: Indepth
Output type: technical

Question:
Review this AI invoice assistant design. It can read invoice emails, open attachments, compare spreadsheet rows, draft vendor replies, and update a shared tracker.
```

## What The Result Includes

Every review uses the same audit structure:

- Immediate answer
- Decision summary
- Red, Orange, Yellow, Green, and Gray finding sections
- Evidence, known safe facts, unknowns, assumptions, and redactions
- Required action, owner routing, safer alternative, and documentation guidance
- Pass/fail explanation and notes

The color model is:

- Red: blocking risk
- Orange: needs owner review
- Yellow: fix, ticket, or accept
- Green: supported as safe
- Gray: not enough context

## Safe Input Guidance

Do not paste raw sensitive material into the chat. Provide safe summaries instead.

Do not paste:

- Raw secrets, tokens, passwords, private keys, session cookies, or connection strings
- Raw customer records, employee records, private messages, support tickets, or sensitive logs
- Private screenshots, signed URLs, reset links, magic links, or private file paths
- Live credential test results or proof of access

Prefer:

- Redacted snippets
- Synthetic examples
- Data type and exposure surface
- Intended audience
- Owner and approval status
- Access model and retention summary
- Relevant safe configuration summaries

## Evals

This repo includes expectation-based evals to check that the skill keeps behaving correctly as it changes.

```text
evals/
  prompts/
  fixtures/
  expected_checks.md
```

To run an eval manually:

1. Open a prompt from `evals/prompts/`.
2. Paste it into a fresh chat or review session.
3. Compare the result to `evals/expected_checks.md`.
4. Save temporary outputs under `evals/results/` if needed. That path is ignored by git.

Do not judge evals by exact wording. Judge whether the result satisfies the required format and behavior checks.

## Repo Layout

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
- `skill/references/` contains the shared rules and depth-specific guidance.
- `evals/prompts/` contains reusable prompts only.
- `evals/fixtures/` contains sanitized local fixtures.
- `evals/expected_checks.md` contains expected behavior, not golden response text.

## Safety Boundary

This skill provides security review guidance, not legal advice and not authorization to test systems. It should escalate legal, privacy, compliance, credential, production, and sensitive-data uncertainty to the proper owner.
