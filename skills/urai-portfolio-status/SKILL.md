---
name: urai-portfolio-status
description: >
  URai Portfolio Status Analyzer — analyzes all portfolio positions in real-time: live price
  vs. entry, distance from SL, distance from T1, Druckenmiller filter, and defines what is
  urgent. Use whenever the user shows a brokerage screenshot, asks 'what is the portfolio
  status?', 'what about my positions?', 'what is close to Stop Loss?', 'how much am I
  making/losing?'. Also when presenting positions with investment amounts. Triggers on:
  portfolio review, position check, portfolio, position, stop loss, SL hit, entry price.
  ALWAYS pull live prices via urai-live-data before running analysis.
---

# URai Portfolio Status Analyzer — SOVEREIGN PRIME V274+

## Mission

Analyze the status of ALL portfolio positions in real-time and identify:
- What is **CRITICAL** (SL < 3% from price)
- What is **EXCELLENT** (T1 < 5% from price — consider partial trim)
- What is **HEALTHY** (continue holding)
- Druckenmiller filter violation?

---

## STEP 1 — Load Data

1. **Read latest prompt**:
   Glob: /Downloads/המרכבה/URai_V*_SOVEREIGN_PRIME_OPTIMIZED.md
   Extract: GEAR table, Entry prices, SL levels, T1/T2 targets, Active ARMs

2. **Pull live prices** — run urai-live-data for all tickers

3. **Read last portfolio status**:
   /Downloads/המרכבה/דשבורד_חי/מחקרי_לילה/URai_Daily_[LATEST]_Portfolio.md

---

## STEP 2 — Calculate Position Status

For each position, calculate:
- pct_from_entry = (current_price - entry_price) / entry_price × 100
- pct_from_sl = (current_price - sl_price) / current_price × 100
- pct_from_t1 = (t1_price - current_price) / current_price × 100

### Automatic Flags:
- 🔴 CRITICAL_SL:  pct_from_sl < 3%   → SL distance < 3% — URGENT!
- 🟠 NEAR_SL:      pct_from_sl < 8%   → Watch
- 🟢 NEAR_T1:      pct_from_t1 < 5%   → Consider partial trim
- ⭐ AT_T1:        current >= t1       → Consider trim L2
- 🔴 BELOW_ENTRY:  pct_from_entry < 0 → Unrealized loss
- ✅ HEALTHY:      all others          → Continue

---

## STEP 3 — Druckenmiller Filter (LAW_810)

- CORE positions (conviction >= 4): max 15
- SATELLITE positions (conviction < 4): max 10
- TOTAL: max 25
- IF total > 25 → ⚠️ DRUCKENMILLER VIOLATION — list which to close

---

## STEP 4 — Output Format

```
## 💼 Portfolio Status — [DATE] [TIME]
*Account: [ACCOUNT_NUMBER] | Live price update: ✅*

### 🚨 Urgent — Requires Immediate Action
| Ticker | Price | Entry | SL | From SL | Flag | Action |
...

### ⭐ Near T1 — Consider Trim
...

### ✅ Healthy Positions
| Ticker | Price | Entry | +/-% | SL | T1 | From T1 | GEAR | Account |
...

### 📊 Portfolio Summary
- Total positions: X / 25 (Druckenmiller)
- CORE: X / 15 | SATELLITE: X / 10
- Unrealized P&L: +/-₪X,XXX (+/-X%)
- Performance since avg entry: X%
```

---

## URai Accounts (V274)

| Number | Name | Currency | Type |
|--------|------|----------|------|
| 778-563707 | Main portfolio | ₪ + USD | Main |
| 778-214501 | USD portfolio | USD | Equity US |
| 778-194991 | Israeli portfolio | ₪ | TASE + US |
| 778-193987 | Small portfolio | ₪ + USD | Mixed |

---

## SL/Entry/Target Definitions — V274

| Ticker | Account | Entry | SL | T1 | T2 | GEAR |
|--------|---------|-------|-----|-----|-----|------|
| GLD | 707 | $440 | $415 | $460 | $490 | 3/5 |
| GDX | 707 | $75 | $78 | $92 | — | 4/5 |
| GDXJ | 707 | $90 | $100 | $125 | — | 4/5 |
| NEM | 707 | $80 | $92 | $115 | — | 4/5 |
| PAAS | 707/991 | $55 | $47 | $58 | $68 | **5/5** |
| AG | 707 | $22 | $17.50 | $23 | $28 | **4/5** |
| EQT | 501 | $48 | $58 | $70 | $75 | 5/5 |
| CTRA | 501 | $31 | $29 | $40 | $48 | 4/5 |
| KTOS | 991 | $90 | $82 | $110 | $130 | 4/5 |
| LMT | 991 | $580 | $610 | $700 | $760 | 4/5 |
| RTX | 991 | $185 | $190 | $220 | $240 | 4/5 |
| PLTR | 987 | $130 | $140 | $175 | $200 | 4/5 |
| ASML | 707 | $1,200 | $1,280 | $1,500 | — | 4/5 |
| CF | 501 | $118 | $115 | $140 | — | 3/5 |
| ESLT | 707/991 | $730 | $820 | $980 | $1,100 | 5/5 |

*Update automatically from latest prompt if values changed.*

---

## Relevant Laws
- **LAW_810** — Druckenmiller Position Count (max 25)
- **LAW_871** — War-Inflation PM Paradox (HOLD during crash)
- **LAW_872** — Silver $70 Floor Defense (accumulate, don't sell)

---

*URai SOVEREIGN PRIME V274+ | urai-portfolio-status | ZERO-LOSS*
