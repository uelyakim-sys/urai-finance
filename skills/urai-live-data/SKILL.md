---
name: urai-live-data
description: >
  URai Live Market Data Puller — pulls live real-time prices for all URai Watchlist tickers.
  MANDATORY: Use whenever the user asks about stock prices, gold price, silver, oil, VIX, bond
  yields, or any question requiring current market data. NEVER answer market price questions
  from memory or cache — always pull live data first. Triggers on: price, quote, live, now,
  today, how much does it cost, what is, current price, watchlist scan, portfolio check,
  any mention of a ticker symbol with a question about its value. CRITICAL: if user shows
  a brokerage screenshot and asks about trades — pull live prices BEFORE answering.
---

# URai Live Market Data — SOVEREIGN PRIME V274+

## Mission

Always — **always** — before any investment analysis, buy/sell recommendation, or portfolio review:
1. Pull live prices from Alpha Vantage
2. Pull live macro from FRED
3. Search spot price for gold + silver + oil via WebSearch

**Never answer from yesterday's prices or memory.**

---

## STEP 1 — Define the List

### URai Full Watchlist (V274)
- Equity US: GLD, GDX, GDXJ, NEM, PAAS, AG, EQT, CTRA, KTOS, LMT, RTX, PLTR, ASML, CF
- TASE: ESLT (Elbit Systems), DLEKG (Delek Group)
- Special: IONQ (quantum), NVDA (AI + helium risk)

### FRED Macro Series
- VIXCLS = VIX Fear Index
- DGS10 = 10Y Treasury Yield
- DGS2 = 2Y Treasury Yield

---

## STEP 2 — Data Pull (all parallel)

### Alpha Vantage — call for each ticker with mcp__alpha-vantage__TOOL_CALL:
tool_name = "GLOBAL_QUOTE", arguments = {"symbol": "<TICKER>"}
**Pull all tickers in one parallel call** — don't wait between tickers.

### FRED Macro — call with mcp__fred__series_FREDSeriesObservations:
- series_id = "VIXCLS" | sort_order = "desc" | observation_start = [14 days ago]
- series_id = "DGS10" | sort_order = "desc" | observation_start = [14 days ago]
- series_id = "DGS2" | sort_order = "desc" | observation_start = [14 days ago]

### WebSearch — spot prices (not in Alpha Vantage):
- "gold spot price today [DATE]"
- "silver spot price today [DATE]"
- "brent crude oil price today [DATE]"

---

## STEP 3 — Standard Output Format

```
## 📊 Live Market Data — [DATE] [TIME IST]
*Source: Alpha Vantage + FRED + WebSearch | Updated: [timestamp]*

### 🪙 Precious Metals & Miners
| Ticker | Price | Change $ | Change % | GEAR | SL | From SL% | Note |
| GLD    | $XXX  | +/-$X    | +/-X%    | 4/5  | $415 | X%    | Gold ETF |
...

### ⚡ Energy
...

### 🛡️ Defense
...

### 📊 Macro
| Series | Value | Date | Weekly Change | Signal |
| VIX    | XX    | ...  | +/-X          | ⚠️/✅ |
| 10Y    | X.XX% | ...  | ...           | ... |
| 2Y     | X.XX% | ...  | ...           | ... |
| Spread | X.XX% | ...  | ...           | ... |

### 🌍 Spot Prices (WebSearch)
| Asset  | Spot Price | Change % | ARM Alert |
| Gold   | $X,XXX     | X%       | ARM_68 status |
| Silver | $XX        | X%       | ARM_54 + LAW_872 |
| Brent  | $XXX       | X%       | LAW_870 status |
```

---

## STEP 4 — Automatic ARM Alerts

After receiving data, automatically check:

### ARM_68 — Inflation-PM Paradox (LAW_871 trigger)
IF gold_change_48h < -5% AND VIX > 25 → ACTIVATE ARM_68 → CONTRARIAN BUY SIGNAL

### ARM_64 — VIX Re-Spike
IF VIX > 25 → ARM_64 ACTIVE → risk-off environment
IF VIX < 20 FOR 5 days → ARM_64 deactivates

### LAW_870 — Energy War Protocol
IF Brent > $95 AND war_active → ENERGY WAR PROTOCOL ON → EQT/CTRA MAX

### LAW_872 — Silver $70 Floor
IF silver_spot < $72 → CHECK: COMEX coverage + CFTC positioning + physical dealers
IF all conditions met → MAXIMUM ACCUMULATION ZONE

---

## Common Errors — How to Handle

| Error | Fix |
|-------|-----|
| Alpha Vantage timeout | Retry once, then WebSearch |
| FRED series not found | Try different observation_start (not limit) |
| Gold series not working | Use WebSearch for gold |
| Alpha Vantage rate limit | Wait 12 seconds, retry |

---

## Entry/SL Reference (V274)

| Ticker | Entry | SL | T1 | T2 | GEAR |
|--------|-------|-----|-----|-----|------|
| GLD | $440 | $415 | $460 | $490 | 3/5 |
| EQT | $48 | $58 | $70 | $75 | 5/5 |
| PAAS | $55 | $47 | $58 | $68 | 5/5 |
| AG | $22 | $17.50 | $23 | $28 | 4/5 |
| KTOS | $90 | $82 | $110 | $130 | 4/5 |
| ASML | $1,200 | $1,280 | $1,500 | — | 4/5 |
| PLTR | $130 | $140 | $175 | $200 | 4/5 |
| LMT | $580 | $610 | $700 | $760 | 4/5 |
| RTX | $185 | $190 | $220 | $240 | 4/5 |
| ESLT | $730 | $820 | $980 | $1,100 | 5/5 |

---

*URai SOVEREIGN PRIME V274+ | urai-live-data | ZERO-LOSS | PRE-APPROVED*
