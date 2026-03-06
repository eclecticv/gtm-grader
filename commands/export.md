# Command: export

Run both the 47-rule SaaS optimization analysis and the 9-check positioning analysis, then produce a comprehensive combined markdown document with every rule from both analyses. Designed as a systematic working document.

## Usage
```
/gtm-grader:export <url>
```

## What It Does

1. **Run the full grade analysis internally** — follow all steps from the `grade` command (crawl homepage + pricing page, screenshot both, read all 4 saas-grader reference files, score all 47 rules)
2. **Run the full position analysis internally** — follow all steps from the `position` command (the homepage is already crawled and screenshotted; read both positioning reference files, score all 9 checks)
3. **Write the comprehensive combined analysis** to a single markdown file in the current directory

## Output

Write a markdown file to the current working directory named `[company-name-lowercase]-gtm-export.md`.

The file must follow this EXACT structure:

```markdown
# GTM Export: [Company Name]

**URL:** [url]
**Date:** [date]
**Overall Score:** [total pass]/[total applicable] across 56 checks ([overall grade])

---

## Summary

| Section | Score | Grade |
|---------|-------|-------|
| **SaaS Optimization** | | |
| Brand & Messaging | X/Y | [grade] |
| Page Design & Visuals | X/Y | [grade] |
| Pricing Plans | X/Y | [grade] |
| Free Trials | X/Y | [grade] |
| Freemium | X/Y | [grade] |
| Churn Prevention | X/Y | [grade] |
| Affiliates | X/Y | [grade] |
| Referrals | X/Y | [grade] |
| **Positioning** | | |
| Dunford Canvas | X/Y | [grade] |
| Fletch Questions | X/Y | [grade] |

---

# Part 1: SaaS Optimization (47 Rules)

## 1. Brand & Messaging ([X/Y] — [Grade])

### BM-1: Productize Your Headline

**What it is:** [Copy from reference — word for word]

**Why it matters:** [Copy from reference — word for word]

**Source:** [Copy from reference — word for word]

**Compliance:** PASS | FAIL | N/A

**Observation:** [Specific observation]

**How to fix:** [Only if FAIL]

---

[...repeat for every rule through RF-5...]

# Part 2: Positioning (9 Checks)

## 9. Dunford Canvas ([X/Y] — [Grade])

### DC-1: Competitive Alternatives Acknowledged

[...same format as above...]

---

[...repeat through FQ-4...]
```

## Critical Rules for the Output

1. **Every single rule and check gets its own section** — all 56 items, no exceptions
2. **"What it is" and "Why it matters" are copied word-for-word** from the reference files
3. **"Source" is the full citation** from the reference files
4. **"Observation" is specific** — quote actual content from the site
5. **"How to fix" is actionable** — concrete alternatives, not vague advice
6. **N/A items are still listed** with explanations
7. **Section grades count only applicable items** — N/A excluded from denominator
8. **The horizontal rule `---` separates every rule/check**
9. **Part 1 and Part 2 are clearly labeled** with their own headers
10. **Section numbering is continuous** — SaaS sections 1-8, Positioning sections 9-10

## After Writing the File

After writing the `.md` file, output a brief terminal summary:

```
EXPORT COMPLETE: [Company Name]
File: [filename].md (56 checks evaluated)

  SaaS Optimization:
    Brand & Messaging     [grade]  (X/Y)
    Page Design           [grade]  (X/Y)
    Pricing Plans         [grade]  (X/Y)
    Free Trials           [grade]  (X/Y)
    Freemium              [grade]  (X/Y)
    Churn Prevention      [grade]  (X/Y)
    Affiliates            [grade]  (X/Y)
    Referrals             [grade]  (X/Y)

  Positioning:
    Dunford Canvas        [grade]  (X/Y)
    Fletch Questions      [grade]  (X/Y)

  OVERALL               [grade]  (X/Y passing)

Open [filename].md for the full analysis.
```

## Notes

- **IMPORTANT: Do NOT use the browser MCP for screenshots.** Always use local headless Chrome via the Bash tool instead.
- The export file is the most comprehensive output — it covers all 56 checks in full detail
- For a quick overview, use `/gtm-grader:wins` instead
- For SaaS optimization only, use `/gtm-grader:grade`
- For positioning only, use `/gtm-grader:position`
- If Chrome is not installed, proceed with text-only analysis
- The `.md` file should be a complete, standalone document suitable for systematic client work
