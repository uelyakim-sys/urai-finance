---
name: urai-gear
description: >
  URai GEAR Hunter Scanner — scans the full Watchlist and calculates GEAR score (1-5) for each
  ticker with live prices. Shows TOP 3 opportunities today by GEAR + price in entry range.
  Use for: 'what is worth buying today?', watchlist scan, 'what is the GEAR of X?', 'what is
  best to invest in now?', Hunter analysis, sector scan, 'what are the strongest tickers?',
  opportunity finder. ALWAYS pulls live prices first. Triggers on: GEAR, Hunter, watchlist,
  opportunity, what to buy, scan, best pick, top ticker, sector analysis, weekly scan.
---

# URai GEAR Hunter Scanner — SOVEREIGN PRIME V274+

## What is GEAR?

**GEAR = Global Event Alignment Ranking** (1-5):
Score that weights: Fundamental thesis + Technical setup + Active LAWs + ARM signals + Timing

- GEAR 5/5 = MAX CONVICTION — all stars aligned
- GEAR 4/5 = HIGH — strong thesis, good entry
- GEAR 3/5 = MEDIUM — thesis correct but timing/risk not ideal
- GEAR 2/5 = WEAK — wait for better setup
- GEAR 1/5 = AVOID

---

## STEP 1 — Pull Live Prices

Run urai-live-data for all tickers simultaneously:
- Equity US: GLD, GDX, GDXJ, NEM, PAAS, AG, EQT, CTRA, KTOS, LMT, RTX, PLTR, ASML, CF
- TASE: ESLT, DLEKG (WebSearch since Alpha Vantage doesn't support TASE)
- Optional: IONQ, NVDA

---

## STEP 2 — Read Active ARMs

Glob: /Downloads/המרכבה/URai_V*_SOVEREIGN_PRIME_OPTIMIZED.md
Extract: Active ARMs, GEAR table, LAW triggers

### ARMs affecting GEAR (V274):
| ARM | Status | Effect |
|-----|--------|--------|
| ARM_53 GIAP (Iran/Israel) | 96/100 ACTIVE | +1 GEAR for defense, +1 for energy |
| ARM_54 CFTC Silver | MAX ACTIVE | +1 GEAR for PAAS, AG |
| ARM_62 Clive Thompson | ACTIVE | +1 GEAR for PAAS, AG (COMEX drain) |
| ARM_64 VIX Re-Spike | ACTIVE (VIX>25) | -1 GEAR for risk assets, +1 for GLD/SL |
| ARM_68 PM Paradox | ACTIVE | +1 GEAR for GLD, PAAS, AG (contrarian) |
| LAW_870 Energy War | ACTIVE | +1 GEAR for EQT, CTRA, LMT |
| LAW_872 Silver Floor | ACTIVE | +1 GEAR for PAAS, AG (max accumulate) |

---

## STEP 3 — Calculate GEAR for each ticker

### GEAR Calculation Matrix:
- base_gear = fundamental_thesis (1-3)
- arm_bonus = sum(active ARMs that directly affect this ticker)
- timing = 1 if current_price IN entry_range else 0
- momentum = 1 if 5d_change > +3% else -1 if 5d_change < -8%
- final_gear = min(5, max(1, base_gear + arm_bonus + timing + momentum))

### Base GEAR Reference (V274):
| Ticker | Base | ARM bonus | Notes |
|--------|------|-----------|-------|
| EQT | 4 | +1 (LAW_870) | ATH, LNG dominance |
| PAAS | 3 | +2 (ARM_54+62+68+LAW_872) | Silver floor |
| AG | 3 | +2 (ARM_54+LAW_872) | Silver miners |
| KTOS | 4 | +1 (ARM_53) | Defense, war |
| LMT | 3 | +1 (ARM_53) | Defense, missiles |
| RTX | 3 | +1 (ARM_53) | Defense |
| PLTR | 4 | +0 | AI defense, strong |
| GLD | 3 | -1 (crash) | FOMC headwind |
| ASML | 4 | 0 | Semi recovery |
| CTRA | 3 | +1 (LAW_870) | Gas/energy |
| ESLT | 5 | +1 (ARM_53) | Israeli defense, ATH |

---

## STEP 4 — Entry Range Check

- IN_RANGE: current_price BETWEEN (entry × 0.95) AND (entry × 1.05)
- ABOVE_RANGE: current_price > entry × 1.05
- BELOW_RANGE: current_price < entry × 0.95 (near SL — caution)
- AT_SL: current_price < entry × 0.97 (danger zone)

---

## STEP 5 — Standard Output

```
## 🔍 URai GEAR Scanner — [DATE] [TIME]
*Live prices: ✅ | Updated ARMs: ✅*

### 🏆 TOP 3 Opportunities Today (GEAR ≥ 4 + IN RANGE)

**#1 [TICKER] — GEAR [X]/5** ⭐⭐⭐⭐⭐
- Price: $[PRICE] | Entry: $[ENTRY] | SL: $[SL] | T1: $[T1]
- Status: [IN RANGE / ABOVE / BELOW]
- ARMs: [list active]
- Thesis: [1-2 lines]
- Action: [BUY / ADD / HOLD] | Level: [L1/L2]

### 📊 Full Watchlist
| Ticker | GEAR | Price | Entry | Status | Daily Change | SL | ARMs | Note |
...

### 🚨 Warnings
[Any position near SL, any GEAR downgrade, any new ARM activation]
```

---

## GEAR Auto-Update

After each scan, note if anything changed:
- If ticker changed entry/SL/GEAR from last scan → note reason
- Feeds back into next nightly research cycle

---

*URai SOVEREIGN PRIME V274+ | urai-gear | GEAR Scanner | Hunter Watchlist*
