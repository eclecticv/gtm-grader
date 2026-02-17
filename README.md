# SaaS Grader

Score any SaaS website against 47 optimization rules drawn from published research in the *Journal of Marketing*, *Journal of Consumer Research*, *Marketing Science*, *Management Science*, and 10+ other peer-reviewed journals — conducted at UCLA, Stanford, MIT Sloan, University of Melbourne, NUS, Georgetown, and Nielsen Norman Group, among others.

Every rule includes the full citation. No opinions, no best-practice hand-waving — just the science and a PASS/FAIL verdict.

## Installation

```bash
# Load the plugin from its directory
claude --plugin-dir /path/to/saas-grader
```

Or add to your Claude Code settings for persistent loading.

## Commands

### `/analyze <url>`

Analyzes a SaaS website against all 47 rules and exports a comprehensive markdown report.

```
/saas-grader:analyze https://example.com
```

**Output:** A standalone `.md` file (`example-saas-analysis.md`) covering every rule with:
- What the rule is and why it matters (from research)
- Full academic citation (authors, journal, universities)
- PASS/FAIL/N/A compliance verdict
- Specific observation from the site
- Concrete fix recommendation (if failing)

### `/report <url>`

Runs the same analysis and generates a polished PDF summary report.

```
/saas-grader:report https://example.com
```

**Output:** A designed A4 PDF saved to your current directory.

## What It Checks (47 Rules)

| # | Category | Rules | Examples |
|---|----------|-------|---------|
| 1 | Brand & Messaging | BM-1 to BM-8 | Productized headline, top 3 benefits, present tense, newness, simple language, social proof numbers, star rating, curated testimonial |
| 2 | Page Design & Visuals | PD-1 to PD-14 | Design-product fit, brand colors, layout adaptation, complexity, rounded CTAs, machine font, CTA placement, before/after flow, video usage, above-the-fold, succinctness, scannable structure, signal-to-noise |
| 3 | Pricing Plans | PR-1 to PR-9 | 3-5 plans, decoy plan, left-to-right ordering, price below features, difference framing, simple pricing, easy math, flat+usage hybrid, flat-rate option |
| 4 | Free Trials | FT-1 to FT-4 | Full-feature trial, 7-day length, high trial usage, extensions over discounts |
| 5 | Freemium | FM-1 to FM-2 | Usage-limited freemium, freemium decoy plan |
| 6 | Churn Prevention | CP-1 to CP-3 | Customer gifts, auto-enrolling loyalty, generous downgrades |
| 7 | Affiliates | AF-1 to AF-2 | Optimize affiliate payment model, protect from deceptive affiliates |
| 8 | Referrals | RF-1 to RF-5 | Altruistic framing, pre-filled messages, avoid money rewards, keep rewards small, targeted referrals |

## Requirements

- Claude Code CLI
- Browser MCP (for screenshots and PDF generation)
- WebFetch capability (for page content extraction)

## File Structure

```
saas-grader/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── analyze.md
│   └── report.md
├── skills/
│   └── saas-grader/
│       ├── SKILL.md
│       └── reference/
│           ├── brand-messaging.md
│           ├── page-design.md
│           ├── pricing-plans.md
│           └── growth-levers.md
├── assets/
│   └── report-template.html
└── README.md
```
