---
name: openclaw-equity-research
description: Use this skill when the user asks for stock analysis, equity research, company research, ticker research, investment memo drafting, BUY/SELL/HOLD style research, watchlist triage, catalyst/risk analysis, valuation framing, or an OpenClaw agent workflow for public equities.
---

# OpenClaw Equity Research

## Goal
Produce decision-ready equity research that combines market data, company context, catalysts, valuation framing, risk checks, and an explicit evidence trail.

This skill is inspired by:
- OpenBB as the data-platform pattern: connect data once, consume it in reports, terminals, dashboards, or agents.
- Agentic stock research systems as the workflow pattern: split work into stock finder, market data, news/catalyst, and recommendation synthesis stages.

## Use Cases
- Single ticker research memo: `AAPL`, `TSLA`, `NVDA`, `RKLB`, etc.
- Watchlist triage: compare multiple tickers and rank research priority.
- Company deep dive: business model, market structure, financial quality, catalysts, valuation, risks.
- Trading-oriented note: technical setup, levels, momentum, stop/risk framing.
- Long-term investor note: moat, growth, margins, capital allocation, valuation scenario.
- OpenClaw workflow design for analyst teams, research terminals, or agentic investment workspaces.

## Hard Rules
- Do not present output as financial advice. Use research language, not instructions to trade.
- Separate facts, estimates, and judgment.
- Cite or name sources for all nontrivial claims when sources are available.
- Prefer fresh data. For current prices, news, estimates, filings, and analyst changes, browse or use data APIs unless the user explicitly forbids it.
- If data is stale, missing, or provider-limited, say so in the memo.
- Do not fabricate financial metrics, target prices, filings, analyst ratings, or news.
- For high-stakes recommendations, include bear case, key downside risks, and what would falsify the thesis.

## Quick Start
From this skill directory:

```bash
python3 scripts/equity_research.py AAPL --out reports
python3 scripts/equity_research.py TSLA NVDA RKLB --mode watchlist --out reports
python3 scripts/equity_research.py --template AAPL --out reports
```

The script writes:
- `{ticker}-equity-research.md`
- `{ticker}-equity-research.json`
- or `watchlist-equity-research.md` for multi-ticker triage

## Research Workflow
1. Clarify scope only when necessary: ticker(s), market, time horizon, user intent, and risk tolerance.
2. Gather data:
   - price history, volume, technical posture
   - company profile, sector, market cap
   - recent news/catalysts
   - fundamentals and valuation metrics when available
   - filings/transcripts/earnings if the user needs a deep dive
3. Run the stage model:
   - **Finder/Triage**: why this ticker is in scope and what makes it worth research time.
   - **Market Data**: price, trend, liquidity, volatility, technical levels.
   - **News/Catalyst**: recent events, sentiment, near-term calendar.
   - **Fundamental/Valuation**: revenue quality, margin trend, cash generation, balance sheet, multiples or scenario frame.
   - **Synthesis**: base case, bull case, bear case, key risks, monitoring points.
4. Produce a memo with an explicit evidence table and confidence level.
5. If the user asks for an action label, use `Research View: Bullish / Neutral / Bearish`, not personalized investment advice.

## Output Shape
Use this memo structure unless the user requests a different format:

```markdown
# {TICKER} Equity Research Memo

## Snapshot
- Research view:
- Time horizon:
- Current price / market cap:
- Data timestamp:
- Confidence:

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
- Key assumptions:

## Risks And Falsification

## Monitoring Checklist

## Research Limits
```

## When To Load References
- Read `references/research-framework.md` before writing a full memo, building an agent workflow, or modifying the script.
- Read `references/data-sources.md` when choosing between OpenBB, yfinance, SEC/filings, news, or web sources.
- Read `references/report-rubric.md` when the user asks for institutional quality or review-ready output.

## Script Notes
`scripts/equity_research.py` is intentionally lightweight:
- OpenBB-style design: one script produces reusable JSON + markdown artifacts.
- yfinance-first runtime because it is already available in many OpenClaw environments.
- OpenBB can be added later as a provider layer without changing the memo contract.
- The script's output is a research starting point; the agent should still add judgment, source checks, and user-specific context when requested.
