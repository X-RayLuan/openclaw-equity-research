# OpenClaw Equity Research

**Analyst-grade equity research workflows for OpenClaw.**

`openclaw-equity-research` helps OpenClaw turn public-company inputs into review-ready equity research artifacts: earnings previews, post-earnings updates, model update notes, initiating coverage drafts, sector overviews, catalyst calendars, thesis trackers, idea screens, and ticker memos.

It is designed for research assistance and analyst workflow automation. It is not financial, legal, tax, accounting, or trading advice.

---

## What changed in 0.1.2

The skill was rewritten from a simple ticker memo helper into a broader equity research workflow layer:

- added earnings preview and earnings analysis workflows
- added model update, initiating coverage, sector overview, catalyst calendar, thesis tracker, and idea-generation flows
- added source-quality rules for filings, transcripts, investor relations materials, market data, and reputable secondary sources
- added explicit guardrails for stale data, unsupported claims, valuation assumptions, and human review
- added Codex/OpenClaw routing guidance for spreadsheets, documents, presentations, and web research
- added two new references: `references/workflows.md` and `references/research-standard.md`

The older lightweight script and original reference files remain in the repo for fast ticker memo generation and future provider-layer work.

---

## Best for

- earnings previews before a company reports
- post-earnings updates after a release, call, or filing
- model update notes with changed assumptions and valuation implications
- initiating coverage drafts
- sector and thematic overviews
- catalyst calendars and thesis trackers
- long/short idea screens and watchlist triage
- single-ticker research memos

---

## Research standard

The skill pushes OpenClaw toward a consistent analyst note standard:

- **Snapshot** — company, ticker, date, source freshness, currency, and market data timestamp
- **Key takeaways** — what changed, why it matters, and what to watch
- **Evidence table** — metric or event, source, reported value, comparison point, and implication
- **Model and valuation assumptions** — drivers, ranges, sensitivities, and conclusion-changing inputs
- **Risks and counterarguments** — the strongest opposing case and missing diligence
- **Source list** — links or local files for material claims
- **Human review note** — checks needed before external use

---

## Source policy

For current facts, OpenClaw should browse or use connected data sources. The skill prefers:

1. Company filings, investor relations releases, earnings presentations, transcripts, and official websites
2. Exchange and regulator sources
3. User-provided models, notes, datasets, and vendor exports
4. Reputable financial press or analyst summaries for context and triangulation

The skill tells OpenClaw not to invent consensus estimates, market prices, valuation multiples, target prices, management commentary, or filing data. If data is stale, missing, or provider-limited, the output should say so.

---

## Example prompts

```text
Use OpenClaw Equity Research to write an earnings preview for NVDA.
```

```text
Prepare a post-earnings update for TSLA with reported KPIs, guidance changes, model implications, and risks.
```

```text
Build a catalyst calendar for AMD and NVDA for the next two quarters.
```

```text
Draft an initiating coverage outline for RKLB with valuation framework and thesis kill criteria.
```

```text
Compare PLTR and SNOW as an idea-generation screen with evidence, counterarguments, and next diligence.
```

---

## Included workflows

### Earnings preview

Maps consensus, guidance, buyside debate, key KPIs, likely stock-moving questions, and bull/base/bear print scenarios.

### Earnings analysis

Reads the release, presentation, transcript, and filing; compares actuals to expectations or prior guidance; isolates beats, misses, guide changes, margin drivers, cash flow, segment trends, and management tone.

### Model update

Rolls forward periods, imports actuals, updates drivers, rebuilds valuation and sensitivity tables, and documents every changed assumption.

### Initiating coverage

Structures the investment summary, company profile, industry map, competitive position, financial drivers, valuation framework, catalysts, risks, and appendix.

### Sector overview

Covers value chain, demand and supply drivers, regulation, technology, pricing, peer comparison, valuation dispersion, and likely winners or losers under key scenarios.

### Catalyst calendar and thesis tracker

Turns dated events and thesis claims into monitored rows with source, confidence, evidence, counterevidence, kill criteria, and next action.

### Idea generation

Screens for dislocations, estimate revisions, valuation versus quality, margin inflection, refinancing risk, short interest plus catalysts, ownership changes, product cycles, regulation, or litigation.

---

## Files

- `SKILL.md` — agent-facing routing, output contract, tool guidance, and guardrails
- `references/workflows.md` — detailed workflow checklists
- `references/research-standard.md` — source, evidence, calculation, writing, and review standards
- `references/research-framework.md` — original memo framework
- `references/data-sources.md` — data-provider guidance and caveats
- `references/report-rubric.md` — quality rubric for review-ready output
- `scripts/equity_research.py` — lightweight ticker memo generator
- `agents/openai.yaml` — OpenAI/OpenClaw UI metadata

---

## Quick start for the script

From this skill directory:

```bash
python3 scripts/equity_research.py AAPL --out reports
python3 scripts/equity_research.py TSLA NVDA RKLB --mode watchlist --out reports
python3 scripts/equity_research.py --template AAPL --out reports
```

The script writes:

- `{ticker}-equity-research.md`
- `{ticker}-equity-research.json`
- `watchlist-equity-research.md`

The script is intentionally lightweight. It is a starting point for fast memo generation; the skill instructions tell the agent to add fresh sourcing, judgment, assumptions, and review gates when the user needs a research-quality output.

---

## Important limits

This skill does not replace:

- professional investment advice
- compliance review
- full audited financial modeling
- institutional market data terminals
- licensed analyst estimate feeds unless separately connected

Use it as a structured research workflow for drafting, triage, and analysis that a qualified human can review.
