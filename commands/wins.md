# Command: wins

Run both the 47-rule SaaS optimization analysis and the 9-check positioning analysis, then produce a one-page prioritized summary of the most impactful findings. Designed to be shareable as a free audit teaser.

## Usage
```
/gtm-grader:wins <url>
```

## What It Does

1. **Run the full grade analysis internally** — follow all steps from the `grade` command (crawl homepage + pricing page, screenshot both, read all 4 saas-grader reference files, score all 47 rules)
2. **Run the full position analysis internally** — follow all steps from the `position` command (the homepage is already crawled and screenshotted; read both positioning reference files, score all 9 checks)
3. **Classify every FAIL into priority tiers** based on the criteria below
4. **Write a one-page prioritized summary** to a markdown file in the current directory

## Priority Classification

### Critical (High Impact)
Items that are above the fold, directly block conversion, or have the strongest research effect sizes:
- Headline/positioning misses (BM-1, DC-1, DC-3, FQ-1, FQ-3, FQ-4)
- No social proof or trust signals above the fold (BM-6, BM-7)
- CTA missing or poorly placed (PD-5, PD-7, PD-11)
- Target customer not identified (DC-4, FQ-2)
- Value proposition unclear (DC-2, DC-5)

### Medium (Moderate Impact)
Items that affect conversion but are below the fold or have moderate effect sizes:
- Design-product mismatch (PD-1, PD-2, PD-3)
- Pricing structure issues (PR-1, PR-2, PR-3, PR-6)
- Content structure problems (PD-12, PD-13, PD-14)
- Missing before/after framing (PD-8)
- Testimonial quality (BM-8)

### Low (Nice-to-Have)
Items that are less visible, harder to observe, or have smaller effect sizes:
- Font choices (PD-6)
- Video speed (PD-10)
- Referral framing details (RF-1 through RF-5)
- Affiliate structure (AF-1, AF-2)
- Churn prevention signals (CP-1, CP-2, CP-3)
- Trial length optimization (FT-2, FT-4)

## Output

Write a markdown file to the current working directory named `[company-name-lowercase]-gtm-wins.md`.

The file must follow this EXACT structure:

```markdown
# GTM Quick Wins: [Company Name]

**URL:** [url]
**Date:** [date]
**Score:** [total pass]/[total applicable] across 56 checks ([overall grade])

---

## Critical Fixes

- **[Rule ID]: [Rule Name]** — [One-sentence observation]. Fix: [One-sentence actionable recommendation].
- ...

## Medium Priority

- **[Rule ID]: [Rule Name]** — [One-sentence observation]. Fix: [One-sentence recommendation].
- ...

## Low Priority

- **[Rule ID]: [Rule Name]** — [One-sentence observation]. Fix: [One-sentence recommendation].
- ...

## Top Wins (What's Working)

- **[Rule ID]: [Rule Name]** — [One-sentence observation of what they're doing well].
- ...

---

*Full analysis available via `/gtm-grader:export <url>`*
```

## Critical Rules for the Output

1. **Only include FAILs** in the fix sections — do not list PASSes or N/As as fixes
2. **Only include PASSes** in the Top Wins section — pick the 3-5 strongest passes
3. **Each item is exactly 1-2 lines** — observation + fix on the same line
4. **Total output should be roughly 30-40 lines** of actionable items — this is a one-pager, not a full report
5. **Be specific** — don't say "improve headline." Say what the headline currently says and what it should say instead
6. **Include the rule ID** so the reader can look up the full analysis in the export
7. **If a tier has no FAILs, omit that section** — don't include empty sections

## After Writing the File

After writing the `.md` file, output a brief terminal summary:

```
WINS COMPLETE: [Company Name]
File: [filename].md
Score: X/Y ([grade]) across 56 checks

  Critical fixes:  [N]
  Medium fixes:    [N]
  Low fixes:       [N]
  Top wins:        [N]

Open [filename].md for the prioritized summary.
For the full per-rule analysis: /gtm-grader:export [url]
```

## Notes

- **IMPORTANT: Do NOT use the browser MCP for screenshots.** Always use local headless Chrome via the Bash tool instead.
- The wins file is the primary output — keep it concise and shareable
- This command runs both analyses internally but only outputs the one-page summary, not the detailed reports
- If Chrome is not installed, proceed with text-only analysis
- Priority classification is a guideline — use judgment for edge cases. An item classified as "Medium" can be elevated to "Critical" if the observation is particularly severe for this specific site.
