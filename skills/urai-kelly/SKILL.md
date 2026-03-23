---
name: urai-kelly
description: >
  URai Kelly Position Sizer — calculates optimal position size using Kelly Criterion,
  Half-Kelly, and Druckenmiller filter. Use whenever the user asks 'how much to buy?',
  'how much to invest?', 'position size', 'what amount?', 'how many shares?'. Also when
  the user specifies a dollar amount and wants to know how to allocate it. Triggers on:
  position sizing, Kelly criterion, how many shares, allocation, portfolio allocation,
  how to split $X, sizing. ALWAYS combine with urai-live-data to get current prices
  before calculating share counts.
---

# URai Kelly Position Sizer — SOVEREIGN PRIME V274+

## Kelly Formula

f* = (p × b - q) / b

Where:
- p = probability of profit (from HGEN consensus, 0-1)
- q = probability of loss = 1 - p
- b = T1/SL ratio from entry price: b = (T1_price - entry_price) / (entry_price - SL_price)

**Half-Kelly = f* / 2** ← URai always uses Half-Kelly

---

## STEP 1 — Gather Data

1. **Live price** (urai-live-data): current_price
2. **From V[LATEST] prompt**: entry, SL, T1, GEAR, active ARMs
3. **HGEN consensus** (if run): bull probability (p)
   - Without HGEN, use GEAR as proxy:
     - GEAR 5/5 → p = 0.75
     - GEAR 4/5 → p = 0.65
     - GEAR 3/5 → p = 0.55

---

## STEP 2 — Calculate Kelly

Example for EQT:
- entry = $48.0, sl = $58.0 (trailing), t1 = $70.0
- p = 0.75 (GEAR 5/5), q = 0.25
- b = (t1 - entry) / (entry - sl) — adjusted for trailing SL
- f_star = (p × b - q) / b
- half_kelly = f_star / 2
- dollar_amount = portfolio_value × half_kelly
- shares = dollar_amount / current_price

---

## STEP 3 — Checks & Flags

**Over-Kelly flag:**
If current_position_value / portfolio_value > f_star → ⚠️ OVER-KELLY — consider Trim

**Under-Kelly + GEAR ≥ 4:**
If current_position_value / portfolio_value < half_kelly AND GEAR >= 4 → 🟢 UNDER-KELLY — opportunity to add

**Druckenmiller check:**
- If total_positions > 25: FLAG violation
- If core_positions > 15: FLAG violation
- If satellite_positions > 10: FLAG violation

---

## STEP 4 — Output Format

```
## 🎯 Kelly Sizing — [TICKER] | [DATE]

Input data:
- Live price: $[PRICE]
- Entry: $[ENTRY] | SL: $[SL] | T1: $[T1]
- HGEN p: [X%] | GEAR: [X/5]
- b ratio: [X.XX]

Calculation:
- Full Kelly: [X%] = $[AMOUNT]
- Half-Kelly (URai standard): [X%] = $[AMOUNT]
- Shares: [N] shares @ $[PRICE] = $[TOTAL]
- Cost in NIS: ₪[AMOUNT] (rate: [RATE])

Flags:
- [Over/Under Kelly status]
- [Druckenmiller status]
- Approval level: [L1/L2/L3]

Full Table — all positions:
| Ticker | GEAR | p | T1 | SL | b | Kelly f* | Half-Kelly | ₪ Size | Status |
```

---

## URai Portfolio Parameters (V274)

| Account | Approx Value | Currency |
|---------|-------------|----------|
| 778-563707 | ₪1,089,000 | ₪ |
| 778-214501 | ~$20,000 | USD |
| 778-194991 | ₪542,000 | ₪ |
| 778-193987 | ₪117,000 | ₪ |

NIS/USD rate: 3.68 (update from live price)

---

## Special Rules

### When user specifies a specific amount ($20,000):
1. Determine: Is $20K the entire portfolio, a portion, or external amount?
2. Calculate shares for 4 allocations (diversify, not all-in)
3. Always keep 20% cash ("powder dry")
4. Max per position: min(Half-Kelly, 30%) of $20K

### Newton Humility on Kelly:
- If f* > 50% → cap at 40% (Kelly assumes perfect probability knowledge)
- If GEAR = 5/5 AND p > 0.80 → Newton caps p at 0.80

### Mandelbrot adjustment:
- Tail risk = (entry_price - sl_price) × 1.5
- Factor into sizing: don't risk more than 5% of portfolio on tail

---

*URai SOVEREIGN PRIME V274+ | urai-kelly | Half-Kelly standard | Druckenmiller filter*
