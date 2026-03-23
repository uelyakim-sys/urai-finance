---
name: urai-trade-decision
description: >
  URai Trade Decision Engine — generates detailed investment plans with live prices, exact share
  counts, Limit Orders, and SL for each position. MANDATORY: Use whenever a user shows a
  brokerage screenshot and asks what to buy, has an amount to deploy, or wants a specific buy
  recommendation. Triggers on: 'I have $X to invest', 'what to buy today', 'how to invest $X',
  'how many shares to buy', trade recommendation, buy signal with amount, portfolio deployment,
  'distribute $X', buying plan, investment plan. CRITICAL: ALWAYS pulls live prices FIRST.
---

# URai Trade Decision Engine — SOVEREIGN PRIME V274+

## CRITICAL RULE

**Step 0 before everything**: Pull live prices with urai-live-data.
**Never recommend price/quantity based on yesterday's prices.**

---

## STEP 1 — Understand Context

Collect:
- How much money? ($X / ₪X)
- Which account? (707 / 991 / 987 / 501 / other)
- What is already held? (from screenshot / latest prompt)
- Goal? (growth / income / hedge / momentum)
- Time horizon? (day / week / months)

---

## STEP 2 — Pull Data (all parallel)

- urai-live-data → live prices for all tickers
- urai-portfolio-status → current holdings + SL alerts
- urai-laws-arm → which ARMs/Laws are active now
- urai-gear → updated GEAR scores

---

## STEP 3 — Selection Principles

### Diversification Rules:
- IF account already has >2 energy positions → prefer defense/PM
- IF account already has >2 PM positions → prefer energy/defense/tech
- IF any position within 3% of SL → DO NOT ADD to that position

### Priority Matrix (V274):
- GEAR 5/5 + ARM active + IN RANGE = TOP PRIORITY (★★★★★)
- GEAR 4/5 + LAW active + IN RANGE = HIGH PRIORITY (★★★★)
- GEAR 4/5 + no active ARM = MEDIUM (★★★)
- GEAR 3/5 = LOW (★★)

### ARMs Multipliers (V274):
- LAW_870 Energy War → EQT, CTRA × 1.5 allocation
- LAW_872 Silver Floor → PAAS, AG × 1.5 allocation (IF not near SL)
- ARM_53 GIAP → KTOS, LMT, RTX, ESLT × 1.3 allocation
- ARM_68 PM Paradox → GLD add dip × 1.3 allocation

---

## STEP 4 — Calculate Allocation

Total to invest = X dollars. Reserve 20% cash/buffer.
investable = X × 0.80

Recommended positions by amount:
- X < $5,000: 2 positions
- $5,000–$15,000: 3 positions
- $15,000–$30,000: 4 positions
- $30,000+: min(5, remaining Druckenmiller slots)

Kelly sizing per position:
- kelly_pct = calculate_half_kelly(p, b) via urai-kelly
- max_pct = min(kelly_pct, 0.40) — cap at 40% per position of investable
- dollar_amount = investable × max_pct
- shares = floor(dollar_amount / live_price)
- limit_price = live_price × 0.995 (0.5% below current for limit order)

---

## STEP 5 — Full Execution Plan Output

```
## 🎯 URai Trade Plan — $[AMOUNT] | [DATE] [TIME IST]
*Prices: LIVE ✅ | Account: [ACCOUNT]*

### ⚡ Executive: [1 line — why now]

### 📋 Execution Instructions — [N] positions

**1. [TICKER] — GEAR [X]/5 | [★★★★★]**
Action: BUY [N] shares
Live price: $[PRICE] ([+/-X%] today)
Limit Order: $[LIMIT] (0.5% below)
Amount: $[TOTAL] / ₪[NIS_EQUIV]
Mandatory SL: $[SL]
T1: $[T1] (+X%) | T2: $[T2] (+X%)
Rationale: [2 sentences]
ARM/LAW: [what triggers this]

### 💰 Allocation Summary
| Ticker | Shares | Price | Amount | % of Input |
| Reserve | — | — | $[R] | 20% |
| TOTAL | — | — | $[X] | 100% |

### ⏰ Timing
- Now ([TIME] IST): [what can be executed now]
- US Market Open: [if US market closed]
- TASE Open 09:45 IST: [for Israeli positions]

### 🚨 SL Checklist
☐ [TICKER] SL @ $[SL] — enter with the buy
☐ [TICKER] SL @ $[SL] — trailing SL
```

---

## Safety Rules

NEVER recommend:
- A stock whose SL was broken recently (< 2 weeks)
- A stock whose GEAR dropped in last Nightly Research
- Adding to a position already > Half-Kelly

ALWAYS include:
- Limit Order price (not Market Order)
- Exact SL for every position
- L2 reminder if amount > $5,000
- Newton Humility disclaimer: "Markets are full of surprises — no certainty, only probabilities"

---

## Authority Stack
Built by Jake Nesler's $100K Claude Code experiment methodology. 267 iterations. Validated vs. Goldman Sachs price targets.

*URai SOVEREIGN PRIME V274+ | urai-trade-decision | Live prices mandatory | Half-Kelly standard*
