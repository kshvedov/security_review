# Security Review Repo Instructions

## Purpose

This repo contains the clean Security Review Skill package plus expectation-based eval material.

Use `skill/` as the source of truth for the installable skill. Use `evals/` only to test behavior and regression risk.

## Repo Layers

- `skill/SKILL.md`
  - Skill entrypoint and routing instructions.
  - Keep this lean and focused on when to load references.

- `skill/references/`
  - Detailed shared, quick, medium, and indepth guidance.
  - Preserve the required audit output format, classification model, redaction handling, current-source policy, and pass/fail logic.

- `evals/prompts/`
  - Reusable prompt inputs only.
  - Do not save model responses here.

- `evals/fixtures/`
  - Sanitized local fixtures for browser/content review evals.

- `evals/expected_checks.md`
  - Behavior expectations for eval review.
  - Use expectation checks instead of exact golden text.

## Change Rules

- Do not copy research artifacts, staged topic outputs, prompt-layer research kits, old consolidation drafts, or saved response histories into this repo.
- Do not add generated eval responses to tracked files.
- If temporary outputs are needed, save them under `evals/results/` or `evals/runs/`; both are ignored by git.
- Keep eval prompts pointed at `skill/SKILL.md` and `evals/fixtures/...`.
- Keep the skill's required audit format intact across all depths.
- Do not infer whether a user is technical or non-technical; use the requested output type.

## Safety Rules

- Never request or reproduce raw secrets, raw PII, private screenshots, private URLs, raw sensitive logs, customer records, session cookies, tokens, passwords, private keys, or connection strings.
- Redact first, then classify.
- Keep severity separate from confidence.
- Do not classify Green or Pass from assumptions.
- Browser-delivered content should be treated as shared with anyone who can access the page.
- Browser-visible credential-like values are Red/Fail unless clearly fake, public, non-sensitive, and non-usable.
- Do not include exploit payloads, bypass steps, unauthorized testing instructions, credential-use instructions, or legal conclusions.
