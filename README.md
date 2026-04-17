# Career Intelligence Report — Claude Skill

A Claude skill that produces structured, research-backed Career Intelligence Reports for any professional. Upload a resume, describe a background, or just ask — Claude will research the current market and deliver a six-section report covering demand analysis, compensation benchmarks, certifications, a 60-day action roadmap, and a gaps & opportunities assessment.

---

## What It Produces

A full Career Intelligence Report with six sections:

| Section | Contents |
|---|---|
| **Profile Assessment** | Market positioning summary, differentiators, DISC/personality insights if available, location analysis |
| **Market Demand** | 3–4 role titles the person is competitive for, demand signals, target industries |
| **Compensation Benchmarks** | Salary table by role with base, bonus %, total cash, and source citations |
| **Certifications & Skills** | Ranked credentials with cost, time, impact level, and salary premium data |
| **60-Day Action Roadmap** | Phased plan with budget breakdown, specific platforms and cert names, deliverables checklist |
| **Gaps & Opportunities** | What's costing them now vs. what they're not using |

Output defaults to a markdown response in chat. Ask for `HTML` to get a polished, downloadable single-file report with sticky nav, role cards, compensation table, timeline roadmap, and gap/opportunity cards.

---

## Sample Output

A sample report for a fictional event marketing professional (Jordan M. Ellis, Director of Global Events, Atlanta) is included in [`samples/sample_career_report_event_marketing.html`](samples/sample_career_report_event_marketing.html). It demonstrates the full HTML output format with real 2026 market data.

---

## How to Use It

### Recommended Prompt

Upload your resume (PDF works well) and paste the following:

```
Please run a Career Intelligence Report for me based on my resume.
[Include any relevant links — LinkedIn, personal website, etc.]
My budget for the 60-day improvement plan is $[amount].
I'm looking for [new role / fractional work / salary negotiation / skill development].
Please output it as an HTML file.
```

### What Strengthens the Report

These are optional but meaningfully improve quality:

- **Target industries or company types** — e.g., "I want to stay in fintech" or "open to PE-backed SaaS"
- **Constraints** — remote only, no relocation, minimum compensation, etc.
- **DISC or Clifton Strengths data** — used to sharpen the Gaps & Opportunities section with behavioral insights
- **Personal website or LinkedIn URL** — Claude will pull it to understand your public positioning
- **Budget** — if not provided, Claude defaults to $500–$1,000 and states the assumption

If you don't have a resume ready, you can describe your background in plain text and the skill will work from that.

---

## File Structure

```
career-intel-report/
├── SKILL.md                          # Main skill file
└── references/
    ├── html-report-template.md       # Annotated structure for HTML output
    └── salary-sources.md             # Canonical compensation data sources by role type
```

### Reference Files

**`references/html-report-template.md`** — The structural blueprint for HTML reports. Covers section order, card layouts, color conventions for demand badges and gap/opportunity cards, typography guidelines, CSS approach, and what not to do.

**`references/salary-sources.md`** — A curated list of salary data sources organized by type (primary salary benchmarks, fractional/consulting rates, hiring trend sources, certification value sources). Also includes location adjustment notes for major U.S. markets.

---

## How It Works

The skill runs in five steps:

1. **Intake** — Extracts or asks for role, years of experience, location, skills, and goals. If a resume is uploaded, parses it before asking anything.
2. **Research** — Runs 3–6 web searches minimum for current salary data, hiring trends, and certification market value. Does not rely on training data alone for figures that change year-over-year.
3. **Analysis** — Assesses tenure patterns, title vs. scope mismatches, compensation positioning, and the 2–3 strongest differentiators before writing anything.
4. **Report** — Writes all six sections with every claim tied back to the specific person's background.
5. **Output** — Delivers in chat (markdown) or as a downloadable HTML file on request.

---

## Tone & Standards

The skill is written to produce advisor-quality output, not generic career advice:

- Every gap named includes the mechanism by which it costs the person — not just the label
- Every opportunity named explains why *this person specifically* is positioned for it
- Salary figures are always cited with sources and adjusted for location
- DISC or personality data, when provided, is used throughout — not isolated to one section
- The report avoids padding, filler transitions, and re-stating what was just said

---

## Output Formats

| Format | How to Request |
|---|---|
| Markdown in chat | Default — no request needed |
| HTML file | Say "output as HTML" or "I'd like a downloadable file" |
| Word document | Say "output as a Word doc" — requires the `docx` skill |

---

## Notes

- Salary data is always current — Claude searches live sources at generation time, so figures reflect today's market rather than training cutoff data.
- The skill triggers even for partial requests. If someone asks only about certifications, Claude still runs the full intake to ground the cert recommendations properly, then scopes the output to what was asked.
- Budget and time assumptions are always stated explicitly at the top of the 60-day roadmap section if they weren't provided by the user.
