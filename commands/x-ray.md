---
description: Run Competitor X-Ray on a list of competitors (handles, company names, or URLs)
argument-hint: "@handle1 @handle2 company.com  (or leave blank to be asked)"
---

Use the **competitor-x-ray** skill to research the following competitors: $ARGUMENTS

Follow the skill exactly:
- Normalize each target into a social handle, company name, or website (infer which; chase corrected spellings for mistyped handles).
- Ask me which output format I want (designed PDF / chat / spreadsheet / Word) and whether to anchor the findings against a specific business — unless I already said.
- Research each competitor (fan out in parallel if there is more than one), pulling the quantitative layer and tagging every claim CONFIRMED / REPORTED / INFERRED with sources.
- Deliver per-competitor briefs (ICP / funnel / monetization / numbers / links) plus a cross-competitor synthesis with a threat ranking.

If no competitors were provided above, ask me for the list before doing anything else.
