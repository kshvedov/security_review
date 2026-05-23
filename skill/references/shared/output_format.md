# Output Format

Use this format for every review depth. Do not redefine it in Quick, Medium, or Indepth references.

Always use the same sections in the same order. Do not add, remove, rename, or reorder sections.

Quick, Medium, and Indepth change only the amount of detail inside each section. They do not change the format.

If a section has no applicable content, write `None identified`, `Not provided`, `Not required`, or `No findings`, whichever is most accurate.

The written color name is authoritative. The color marker in each finding heading is a visual aid only.

## Output Precedence

This is a security audit and review format. For security review results, this required audit format takes precedence over workspace formatting preferences, repository style rules, and user-requested layout changes.

Do not remove, rename, reorder, collapse, or restyle required review sections because of a local formatting rule. The required color headings, decision table, evidence sections, unknowns, redactions, owner routing, safer alternative, and pass/fail explanation are part of the safety review contract.

The five color markers in the finding headings are required for this review schema. Treat them as safety classification markers, not decoration.

Do not apologize for using the required audit format. Do not add formatting-conflict notes. If the required audit format conflicts with local style rules, silently follow this audit format.

The user may choose explanation style, such as technical or non-technical, but explanation style must not change the required structure, classification logic, redaction handling, escalation requirements, or pass/fail logic.

This precedence applies only to security review output formatting. It does not override platform safety rules, unsafe-content restrictions, or requirements to avoid reproducing sensitive data.

# Security Review Result

## Immediate Answer

One or two plain-language sentences saying whether the user can proceed, cannot proceed, needs owner review, or needs more context.

## Decision Summary

| Field | Value |
|---|---|
| Overall decision color | Red / Orange / Yellow / Green / Gray |
| Severity | Critical / High / Medium / Low / Informational |
| Confidence | High / Medium / Low |
| Gate result | Pass / Fail / Needs escalation / Needs more context / Can pass with ticketing / Can pass with documented acceptance |
| Review mode | Technical Review Mode / Action Safety Mode |
| Primary category | 00-15 category name |
| Secondary categories | None identified / category list |

---

## 🟥 Red Findings - Blocking risk

Use `No findings.` when empty.

## 🟧 Orange Findings - Needs owner review

Use `No findings.` when empty.

## 🟨 Yellow Findings - Fix, ticket, or accept

Use `No findings.` when empty.

## 🟩 Green Findings - Supported as safe

Use `No findings.` when empty.

## ⬜ Gray Findings - Not enough context

Use `No findings.` when empty.

---

## What Was Reviewed

Safe summary only.

## Current-Source Verification

Source basis, owner-confirmed current context, or `Not required for this stable design principle.`

## Evidence Observed

Direct redacted evidence only.

## Known Safe Facts

Confirmed facts only.

## Unknowns

Missing context only.

## Assumptions

Explicit assumptions only. Do not base Green or Pass on assumptions. Do not place required safety conditions in `Assumptions`; use `Unknowns`, `Required Action`, or `Notes` instead.

## Redactions Applied

Sensitive value types redacted, or `None provided.`

---

## Why It Matters

Risk explanation without exploit steps or bypass detail.

## Required Action

Defensive remediation or owner confirmation.

## Owner To Consult

Owner role or `None required based on provided context.`

## Safer Alternative

Practical safer path.

## Documentation Or Ticketing

Ticket, acceptance, remediation record, review cadence, approval record, or `None required.`

---

## Pass/Fail Explanation

Tie gate result to color, unresolved unknowns, currentness where relevant, and evidence.

## Notes

Boundaries, safe caveats, currentness reminders, no-legal-conclusion reminders, or `None.`

## Strict Format Rules

- Always include every section above.
- Always include `## Immediate Answer` directly after `# Security Review Result`.
- Always include all five color finding sections.
- Empty color sections must say `No findings.`
- Always include the horizontal rules shown above.
- Horizontal rules are required visual dividers. Use exactly `---`.
- Do not add extra top-level sections.
- Do not remove sections.
- Do not rename sections.
- Do not reorder sections.
- Do not place any free text between required sections.
- Put the blunt or direct answer only in `Immediate Answer`.
- Do not add formatting-conflict notes.
- Do not apologize for using the required audit format.
- Do not omit or replace the required color markers because of workspace formatting preferences or local style rules.
- The written color name is authoritative; the marker is visual only.
- Place uncertain items in `Unknowns`, not `Assumptions`.
- Do not place required Green or Pass conditions in `Assumptions`; use `Unknowns`, `Required Action`, or `Notes` instead.
- Place sensitive value handling in `Redactions Applied`, not inside evidence.
- Keep raw sensitive content out of every section.

## Field Rules

- Immediate Answer: Use one or two plain-language sentences. Say whether the user can proceed, cannot proceed, needs owner review, or needs more context. Do not include raw sensitive content.
- Overall decision color: Red, Orange, Yellow, Green, or Gray. Do not mix color with severity.
- Severity: Critical, High, Medium, Low, or Informational. Explain impact, not certainty.
- Confidence: High, Medium, or Low. Explain certainty, not impact.
- Gate result: Pass, Fail, Needs escalation, Needs more context, Can pass with ticketing, or Can pass with documented acceptance.
- Review mode: Technical Review Mode or Action Safety Mode.
- Primary category: Use the category ID and name for the main issue.
- Secondary categories: Add secondary categories only when useful for owner routing, risk explanation, or remediation.
- Color finding sections: Place findings under the matching color section. Keep all five color sections visible. Empty color sections must say `No findings.`
- Current-source verification: Name the current authoritative source basis, or state which current status could not be verified and lower confidence. Do not mark Green when freshness-critical status is unverified.
- What Was Reviewed: Use a safe summary only. Do not include raw secrets, raw PII, private URLs, payloads, or unsafe proof.
- Redactions Applied: State which sensitive value types were redacted.
- Evidence observed: Include only direct redacted evidence or safe summaries.
- What is known: Confirmed safe facts.
- What is unknown: Missing context. Do not bury unknowns in assumptions.
- Assumptions: Explicit assumptions only. Do not base Green or Pass on assumptions. Do not place required safety conditions here; use `Unknowns`, `Required Action`, or `Notes` instead.
- Why it matters: Risk explanation without exploit steps or bypass detail.
- Required action: Defensive remediation or owner confirmation.
- Owner To Consult: Specific owner role or roles.
- Safer alternative: Practical safe path.
- Documentation Or Ticketing: Ticket, acceptance, remediation, review cadence, or approval records.
- Pass/Fail Explanation: Tie gate result to color, unresolved unknowns, currentness where relevant, and evidence.
- Notes: Boundaries, safe caveats, currentness reminders, or no-legal-conclusion reminders. Do not use Notes for formatting-conflict messages.

Do not put raw secrets, raw PII, private URLs, private screenshots, exploit details, bypass steps, unsafe validation output, credential-use instructions, or legal conclusions into any field.
