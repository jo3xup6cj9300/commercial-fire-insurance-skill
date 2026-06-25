---
name: fire-insurance-quote
description: Create and maintain Taiwan commercial fire insurance quote workflows, quote sheets, printable PDF-ready HTML tools, insured-property schedules, insured peril wording, additional cover limits, deductibles, notes, and SB endorsement clause lists. Use when the user asks to build, revise, audit, anonymize, or generate commercial fire insurance quote data, quote forms, fire endorsement selectors, or GitHub-ready fire insurance quote assets.
---

# Fire Insurance Quote

Use this skill for commercial fire insurance quote automation, especially Taiwan agency workflows that combine insured information, property schedules, additional covers, deductibles, catastrophe limits, notes, and SB endorsement clauses.

## Core Workflow

1. Collect or normalize quote inputs:
   - Industry, company name, tax ID, representative, phone, mailing address.
   - One or more insured locations.
   - Per-location insured amounts for building, business decoration, machinery, business personal property, and goods.
   - Building structure, deductible, catastrophe percentage, catastrophe limit, other additional cover percentage, notes, and selected additional covers.
2. Generate or update a quote artifact:
   - Prefer the bundled standalone HTML tool at `assets/commercial-fire-quote-tool.html` for interactive quote creation.
   - For a new customized tool, copy the asset first, then edit the copy.
   - Keep the first screen as the working tool, not a marketing page.
3. Produce quote output:
   - Include insured information.
   - Place "本保險契約所承保之危險事故" before "標的物與保額".
   - Include insured-property schedule with subtotals by location and total fire insured amount.
   - Split the quote summary into 自負額, 天災保額, 天災限額, 附加險, 備註.
   - Include SB 附加條款 and user-added custom clauses.
4. Before sharing or preparing GitHub artifacts, anonymize all customer data.

## Reference Files

Read `references/fire-quote-rules.md` when implementing or revising quote logic, field behavior, additional cover grouping, "含..." parsing, or SB endorsement behavior.

Read `references/privacy-checklist.md` before publishing to GitHub or sharing externally.

## Bundled Asset

`assets/commercial-fire-quote-tool.html` is the current standalone browser tool. It can be opened directly in a browser and printed/saved as PDF.

When editing this asset:
- Preserve Traditional Chinese labels unless the user asks otherwise.
- Keep sample data fake.
- Re-test basic syntax after editing.
- Prefer small, targeted changes that match existing layout and wording.

## Important Domain Rules

- 商火險 is the base policy, not an additional cover. Do not list it in the additional-cover input table.
- Catastrophe covers include 颱風/洪水 and 地震.
- Other additional covers use the "其他附加險比例" default unless an individual row overrides it.
- If individual additional-cover percentages differ, group covers by percentage and summarize the largest group as "其餘附加險種".
- If all other additional covers share the same percentage, output a single "其他附加險比例" row.
- Output money with thousands separators.
- Remove English parenthetical clause names in output; preserve Chinese parenthetical text.

## Validation

For HTML changes, run a syntax check by extracting `<script>` blocks and evaluating them with Node.js, then inspect the output file for key labels requested by the user.
