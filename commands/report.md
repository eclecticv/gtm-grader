# Command: report

Generate a polished PDF report from a SaaS optimization analysis.

## Usage
```
/saas-grader:report <url>
```

## What It Does

1. **Run the full analysis** — same steps as `/analyze`: crawl homepage, find pricing page, screenshot both, read reference files, score all 47 rules
2. **Read the HTML template** from `assets/report-template.html`
3. **Populate the template** by replacing all `{{PLACEHOLDER}}` tokens with actual data:
   - `{{COMPANY_NAME}}` — extracted from the homepage
   - `{{URL}}` — the analyzed URL
   - `{{DATE}}` — today's date
   - Grade cards: `{{BM_GRADE}}`, `{{PD_GRADE}}`, `{{PR_GRADE}}`, `{{FT_GRADE}}`, `{{FM_GRADE}}`, `{{CP_GRADE}}`, `{{AF_GRADE}}`, `{{RF_GRADE}}`
   - Grade classes: `{{BM_GRADE_CLASS}}`, etc. — use `grade-a` for A+/A/A-, `grade-b` for B+/B/B-, `grade-c` for C+/C/C-, `grade-d` for D+/D/D-, `grade-f` for F
   - Pass counts: `{{BM_PASS}}`, `{{BM_TOTAL}}`, etc.
   - Progress bars: `{{BM_PROGRESS}}`, etc. — generate 12 `<span>` blocks, filled or empty proportional to pass rate
   - `{{WINS}}` — HTML for top win findings (2-4 items)
   - `{{FIXES}}` — HTML for top fix findings (3-6 items)
   - `{{UNIVERSITY_LIST}}` — comma-separated list of all universities cited in findings
4. **Write the populated HTML** to a temporary file in the current directory
5. **Open in browser MCP** — navigate to the local HTML file
6. **Generate PDF** using browser_run_code:
   ```javascript
   await page.pdf({ path: '[company-name]-saas-report.pdf', format: 'A4', printBackground: true })
   ```
7. **Clean up** — delete the temporary HTML file
8. **Report success** — tell the user where the PDF was saved

## Template Placeholder Reference

### Header
- `{{COMPANY_NAME}}` — Company name (e.g., "Linear")
- `{{URL}}` — Full URL analyzed (e.g., "https://linear.app")
- `{{DATE}}` — Report date (e.g., "February 17, 2026")

### Grade Cards (repeat for BM, PD, PR, FT, FM, CP, AF, RF)
- `{{XX_GRADE}}` — Letter grade (e.g., "A-", "B+", "C")
- `{{XX_GRADE_CLASS}}` — CSS class: `grade-a`, `grade-b`, `grade-c`, `grade-d`, or `grade-f`
- `{{XX_PASS}}` — Number of passing items (e.g., "5")
- `{{XX_TOTAL}}` — Total applicable items (e.g., "7")
- `{{XX_PROGRESS}}` — 12 span elements like:
  ```html
  <span class="block block-filled"></span>
  <span class="block block-filled"></span>
  ...
  <span class="block block-empty"></span>
  ```

### Findings
- `{{WINS}}` — HTML blocks for top wins:
  ```html
  <div class="finding finding-pass">
    <span class="marker">&#10003;</span>
    <div class="content">
      <span class="code">BM-6</span>
      <span class="observation">Strong social proof — "Trusted by 50,000+ teams"</span>
    </div>
  </div>
  ```

- `{{FIXES}}` — HTML blocks for top fixes:
  ```html
  <div class="finding finding-fail">
    <span class="marker">&#10007;</span>
    <div class="content">
      <span class="code">BM-1</span>
      <span class="observation">Headline is vague — "Transform your workflow"</span>
      <div class="recommendation">Productize with a specific outcome</div>
      <div class="citation">National Univ. of Singapore research</div>
    </div>
  </div>
  ```

### Footer
- `{{UNIVERSITY_LIST}}` — All cited universities, comma-separated (e.g., "UCLA, Stanford, MIT Sloan, University of Melbourne, University of South Florida")

## Progress Bar Generation

For a category with X passing out of Y total:
1. Calculate `filled = Math.round((X / Y) * 12)`
2. Generate `filled` blocks with class `block-filled`
3. Generate `12 - filled` blocks with class `block-empty`

## Notes

- The PDF will be saved to the user's current working directory
- File name format: `[company-name-lowercase]-saas-report.pdf` (e.g., `linear-saas-report.pdf`)
- If browser MCP's `page.pdf()` is not available, save the populated HTML file instead and tell the user they can print it to PDF from their browser
- The report is a visual summary — for the full per-rule analysis, use `/analyze` to get the comprehensive `.md` export
- Always include the brief terminal summary as well (same as /analyze), then mention the PDF location
