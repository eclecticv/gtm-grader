# GTM Grader

Score any SaaS website against 56 research-backed checks covering both **SaaS optimization** (47 rules from peer-reviewed marketing science) and **homepage positioning** (9 checks from Dunford and Fletch PMM). Every check includes its full source citation.

## Commands

| Command | What it does | Output |
|---------|-------------|--------|
| `/gtm-grader:grade <url>` | 47-rule SaaS optimization analysis | `[company]-saas-analysis.md` |
| `/gtm-grader:position <url>` | 9-check positioning diagnostic | `[company]-positioning-analysis.md` |
| `/gtm-grader:wins <url>` | One-page prioritized summary (both) | `[company]-gtm-wins.md` |
| `/gtm-grader:export <url>` | Full combined analysis (both) | `[company]-gtm-export.md` |

## Installation

Add the plugin directory to your Claude Code settings file (`~/.claude/settings.json`):

```json
{
  "permissions": {
    "allow": [
      "mcp",
      "Bash(grep:*)",
      "Read",
      "Write"
    ]
  },
  "plugins": [
    "/path/to/gtm-grader"
  ]
}
```

Or load it for a single session:

```bash
claude --plugin /path/to/gtm-grader
```

### Requirements

- Claude Code CLI
- WebFetch capability (built into Claude Code)
- Google Chrome (for homepage screenshots — optional, text-only analysis works without it)

## What It Checks

### SaaS Optimization (47 Rules)

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

Sources: *Journal of Marketing*, *Journal of Consumer Research*, *Marketing Science*, *Management Science*, and 10+ other peer-reviewed journals. Research from UCLA, Stanford, MIT Sloan, Princeton, NUS, Nielsen Norman Group, and others.

### Positioning (9 Checks)

| # | Category | Checks | Framework |
|---|----------|--------|-----------|
| 9 | Dunford Canvas | DC-1 to DC-5 | Competitive alternatives, unique attributes, value mapping, target customer, market category |
| 10 | Fletch Questions | FQ-1 to FQ-4 | What is it?, Who is it for?, What does it replace?, Why is it better? |

Sources: Dunford, A. *Obviously Awesome* (2019). Pierri, A. & Fralic, R. Fletch PMM (2020-2024).

## Priority Classification (wins command)

The `/wins` command classifies failures into three tiers:

- **Critical** — Above-the-fold items that directly block conversion: headline misses, missing social proof, broken CTA placement, unclear value proposition, unidentified target customer
- **Medium** — Below-the-fold or moderate-impact items: design mismatches, pricing structure issues, content organization problems
- **Low** — Less visible or smaller effect size items: font choices, video speed, referral details, affiliate structure, churn signals

## Extensibility

Future analysis domains (UX, SEO/AEO, social media) follow the same pattern:

1. Create `skills/[domain]/SKILL.md` with category overview
2. Create `skills/[domain]/reference/[framework].md` with individual checks
3. Create `commands/[command-name].md` with the analysis pipeline
4. Update `/wins` and `/export` to include the new domain
5. Update `plugin.json` and this README

## File Structure

```
gtm-grader/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── grade.md          # 47-rule SaaS optimization
│   ├── position.md       # 9-check positioning diagnostic
│   ├── wins.md           # One-page prioritized summary
│   └── export.md         # Full combined analysis
├── skills/
│   ├── saas-grader/
│   │   ├── SKILL.md
│   │   └── reference/
│   │       ├── brand-messaging.md
│   │       ├── page-design.md
│   │       ├── pricing-plans.md
│   │       └── growth-levers.md
│   └── positioning/
│       ├── SKILL.md
│       └── reference/
│           ├── dunford-canvas.md
│           └── fletch-questions.md
└── README.md
```
