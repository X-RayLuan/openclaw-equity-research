# OpenClaw Equity Research

**Decision-ready public equity research for OpenClaw.**

`openclaw-equity-research` turns a ticker into a structured research memo with:

- market data and technical context
- company and segment framing
- recent catalysts
- valuation scenarios
- risks and thesis-falsification triggers
- explicit evidence notes and research limits

It is built for **research assistance**, not financial advice.

---

## Best for

- Single-ticker memos: `AAPL`, `TSLA`, `RKLB`, `NVDA`
- Company deep dives
- Watchlist triage
- Catalyst / risk analysis
- Bull / bear / neutral research framing
- OpenClaw-based analyst or PM workflows

---

## Why this exists

Most stock prompts degrade into one of two bad outcomes:

1. generic summaries with no decision value
2. overconfident hot takes with weak sourcing

This skill pushes OpenClaw toward a better default:

- facts first
- explicit valuation framing
- real downside discussion
- what would change the conclusion
- visible research limits when data is stale or incomplete

---

## Research pattern

This skill combines two ideas:

### 1) OpenBB-style platform thinking
- collect market data, fundamentals, and news once
- keep collection separate from synthesis
- make outputs reusable across reports, dashboards, terminals, and agents

### 2) Agentic stock research workflow
- triage why the ticker matters now
- gather market data
- review news and catalysts
- frame valuation
- synthesize a clear bull / base / bear view

---

## Output shape

A typical memo includes:

- Snapshot
- Thesis
- Evidence table
- Market data and technical setup
- Company and fundamentals
- Catalysts
- Valuation frame
- Risks and falsification
- Monitoring checklist
- Research limits

The goal is to produce something an operator, PM, or analyst can scan quickly.

---

## Example prompts

- `Research RKLB and write an equity research memo.`
- `Give me a TSLA bull / bear / valuation note.`
- `Compare NVDA and AMD for a watchlist.`
- `Write a one-page memo on AAPL focused on catalysts and risk.`
- `Use OpenClaw Equity Research skill to analyze PLTR.`

---

## Quick start

From this skill directory:

```bash
python3 scripts/equity_research.py AAPL --out reports
python3 scripts/equity_research.py TSLA NVDA RKLB --mode watchlist --out reports
python3 scripts/equity_research.py --template AAPL --out reports
```

Outputs:

- `{ticker}-equity-research.md`
- `{ticker}-equity-research.json`
- `watchlist-equity-research.md`

---

## Example memo skeleton

```markdown
# RKLB Equity Research Memo

## Snapshot
- Research view: Bullish / valuation-aware
- Time horizon: 12–24 months
- Current price / market cap:
- Data timestamp:
- Confidence: Medium

## Thesis

## Evidence
| Area | Evidence | Source / timestamp | Interpretation |

## Market Data And Technical Setup

## Company And Fundamentals

## Catalysts

## Valuation Frame
- Base case:
- Bull case:
- Bear case:

## Risks And Falsification

## Monitoring Checklist

## Research Limits
```

---

## Files

- `SKILL.md` — agent-facing routing and behavior
- `scripts/equity_research.py` — lightweight report generator
- `references/research-framework.md` — workflow contract
- `references/data-sources.md` — provider guidance and caveats
- `references/report-rubric.md` — memo quality bar

---

## Source policy

The skill is opinionated about evidence:

- prefer fresh market data
- separate facts from judgment
- do not invent metrics, targets, or analyst views
- disclose stale or missing data
- include key downside risks and what would invalidate the thesis

---

## Current runtime approach

The included script is intentionally lightweight:

- **yfinance-first** for fast public-market pulls
- markdown + JSON output for reuse
- OpenBB-style provider layering can be added later without changing the memo contract

This makes it a practical base for:

- internal analyst tooling
- OpenClaw stock research workflows
- lightweight equity memo generation
- future upgrade into a fuller research workspace

---

## Important limits

This repo does **not** replace:

- professional investment advice
- full financial modeling
- institutional-grade market data terminals
- compliance review
- analyst estimate feeds unless separately connected

Use it as a **structured first-pass research engine**.

---

## Bottom line

If you want OpenClaw to turn a ticker into a structured research memo with catalysts, valuation framing, risks, and falsification triggers, this skill gives you a practical base.
