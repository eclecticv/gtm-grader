# Positioning Grader

A framework-backed analysis tool that scores B2B SaaS homepages against 9 positioning checks drawn from April Dunford's *Obviously Awesome* and Fletch PMM's homepage teardown methodology.

Every check includes the full source citation. No opinions, no best-practice hand-waving — just the frameworks and a PASS/FAIL verdict.

## Purpose

Analyze a B2B SaaS homepage against the Dunford Canvas and Fletch Questions. For each check, the output includes what it is, why it matters (the framework rationale), the source citation, a compliance verdict (PASS/FAIL/N/A), the specific observation, and a concrete fix recommendation if failing. The full analysis is exported as a standalone `.md` file.

## How It Works

1. **Crawl** the homepage via WebFetch (text content extraction)
2. **Screenshot the homepage** using local headless Chrome (full-page capture)
3. **Score every check** — all 9 items, each as PASS, FAIL, or N/A
4. **Export** a comprehensive `.md` report covering every check with full context

Only the homepage is analyzed — positioning is a homepage concern.

## The 9-Check Playbook

### 1. Dunford Canvas (5 checks: DC-1 to DC-5)
Competitive alternatives, unique attributes, value mapping, target customer, market category.
> See [reference/dunford-canvas.md](reference/dunford-canvas.md)

### 2. Fletch Questions (4 checks: FQ-1 to FQ-4)
What is it?, Who is it for?, What does it replace?, Why is it better?
> See [reference/fletch-questions.md](reference/fletch-questions.md)

## Scoring

Each section receives a letter grade (A+ through F) based on the percentage of applicable items that pass. Items marked N/A are excluded from the denominator.

| Grade | Pass Rate |
|-------|-----------|
| A+    | 100%      |
| A     | 90-99%    |
| A-    | 85-89%    |
| B+    | 80-84%    |
| B     | 75-79%    |
| B-    | 70-74%    |
| C+    | 65-69%    |
| C     | 60-64%    |
| C-    | 55-59%    |
| D+    | 50-54%    |
| D     | 45-49%    |
| D-    | 40-44%    |
| F     | Below 40% |

## Output Format

For each of the 9 checks, the `.md` report includes:
- **What it is** — description of the check (from the reference)
- **Why it matters** — the framework rationale (from the reference)
- **Source** — full citation with author, book/methodology, year
- **Compliance** — PASS, FAIL, or N/A
- **Observation** — what was specifically observed on the site
- **How to fix** — concrete, actionable recommendation (only if FAIL)

## Frameworks

- Dunford, A. *Obviously Awesome: How to Nail Product Positioning so Customers Get It, Buy It, Love It* (2019)
- Pierri, A. & Fralic, R. Fletch PMM — "The Homepage Teardown" methodology (2020-2024)
