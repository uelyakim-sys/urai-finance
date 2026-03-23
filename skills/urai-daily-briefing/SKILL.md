---
name: urai-daily-briefing
description: >
  URai Daily Portfolio Briefing — master skill that runs all URai skills in the correct order
  and generates a comprehensive daily report. Automatically runs: live-data + portfolio-status +
  laws-arm + gear + hgen (for critical positions) + kelly. Use for: daily report, morning briefing,
  portfolio review, 'what is happening with the portfolio', daily update, 'what needs to be done
  today'. Also runs automatically as scheduled task at 08:30 IST. Triggers on: daily briefing,
  portfolio review, morning scan, weekly review.
---

# URai Daily Portfolio Briefing — SOVEREIGN PRIME V274+

## Orchestration Order

Run in this order (as much as possible in parallel):

**PARALLEL PHASE 1:**
- urai-live-data (all tickers)
- urai-laws-arm (loads prompt + ARM status)
- WebSearch: "gold price today" + "Iran war today" + "VIX"

**SEQUENTIAL (after Phase 1):**
- urai-portfolio-status (uses live prices from Phase 1)
- urai-gear (uses live prices + ARMs from Phase 1)
- Brier check (uses WebSearch from Phase 1)

**CONDITIONAL (only if needed):**
- urai-hgen (if any position CRITICAL or near T1)
- urai-kelly (if new opportunity or sizing question)

---

## STEP 0 — Load Latest Version

1. Glob: /Downloads/המרכבה/URai_V*_SOVEREIGN_PRIME_OPTIMIZED.md → read latest
2. Glob: /Downloads/המרכבה/URai_Forecast_Log.md → read
3. Glob: /Downloads/המרכבה/דשבורד_חי/מחקרי_לילה/URai_Research_*_2330.md → read latest

Extract: GEAR table, Neural weights, BRIER avg, active forecasts, last changes

---

## STEP 1 — Live Data Pull (parallel)

- Alpha Vantage: GLD, GDX, GDXJ, NEM, PAAS, AG, EQT, CTRA, KTOS, LMT, RTX, PLTR, ASML, CF
- FRED: VIXCLS, DGS10, DGS2 (observation_start = 14 days ago, sort_order = desc)
- WebSearch: "gold spot price today [DATE]"
- WebSearch: "silver spot price today [DATE]"
- WebSearch: "Iran Israel war news [DATE]"
- WebSearch: "Brent crude oil price today [DATE]"

---

## STEP 2 — ARM Status Check

For each critical ARM, check if changed from last Nightly:
- ARM_53 GPR score up/down?
- ARM_64 VIX crossed 20 / 25?
- ARM_68 Gold recovered?
- LAW_870 Brent still >$95?
- LAW_872 Silver still <$72?

---

## STEP 3 — Portfolio Position Check

For each position:
- pct_from_sl = (price - sl) / price × 100
- If pct_from_sl < 3%: CRITICAL — SL at {pct:.1f}%
- If price >= t1: T1 HIT — consider trim L2

---

## STEP 4 — Brier Resolution

For each open forecast in URai_Forecast_Log.md:
- IF resolution_date <= today: WebSearch to check outcome
- Calculate Brier = (P/100 - outcome)^2
- Update: open → closed, add to statistics

---

## STEP 5 — HGEN (Conditional)

Activate urai-hgen ONLY if:
- Position close to SL (< 3%)
- Position reached T1
- Major macro event affecting specific position

---

## OUTPUT — Daily Briefing Report

```
# ⚡ URai Daily Briefing — [DATE] [TIME IST]
## V[N] | Neural Brier: [X.XXX] | [N] Forecasts Open

## 1. EXECUTIVE BRIEF (3 lines)
[Line 1: Most important thing in portfolio today]
[Line 2: Most important macro signal]
[Line 3: One immediate action if required]

## 2. 📊 Live Macro
| Indicator | Value | Change | Signal |
...

## 3. 🔔 Active ARMs
[ARM_53: X/100 | ARM_68: X/4 | ...]

## 4. 💼 Portfolio — Status of all positions
[Quick — flags only]

## 5. ⚖️ HGEN Verdicts (if activated)
[FINCON summaries]

## 6. 🎯 Kelly Alerts
[Over/Under Kelly positions]

## 7. 📋 Brier Updates
[Closed forecasts + new ones]

## 8. 🧠 Neural Update
[Weight changes, ARMs activated/deactivated]

## 9. 🚨 Action List — sorted by urgency
| # | Action | Ticker | Level | Account | Deadline |
| 1 | [L1 AUTO-SL] | PAAS | L1 | 707/991 | Immediate |
```

---

## Save Protocol

Save to: /Downloads/המרכבה/דשבורד_חי/מחקרי_לילה/URai_Daily_[YYYY-MM-DD]_Portfolio.md
Also update: /Downloads/המרכבה/URai_Forecast_Log.md (if Brier closed)

---

## Scheduled Task Integration

This skill runs the scheduled task at 08:30 IST, Sunday–Thursday (before TASE opens at 09:45).
After each Nightly Research: Nightly generates V[N+1] → next day's Daily already uses it.

---

*URai SOVEREIGN PRIME V274+ | urai-daily-briefing | Master orchestrator | 08:30 IST daily*
