---
name: urai-hgen
description: >
  URai HGEN Round Table — runs a "round table" of experts (6 phases) for any position,
  ticker, or investment question. 30 financial experts with updated Neural weights.
  Use this skill for: any buy/sell question on a stock, 'what to do with X?',
  'should I buy Y?', 'should I hold Z?', when a position is near SL, when you need
  FINCON VERDICT, position sizing debate, bull vs. bear analysis.
  ALWAYS pulls live data before running the round table.
  Triggers on: HGEN, round table, buy/sell debate, position review, FINCON verdict request,
  investment thesis debate.
---

# URai HGEN Round Table — SOVEREIGN PRIME V274+

## Mission
Run a **real** expert debate with Bull camp vs Bear camp, cross-examination, and synthesis — to get a clear FINCON VERDICT.

---

## STEP 0 — Pre-Round Table Setup

1. **Pull live price** (urai-live-data) for the selected ticker
2. **Read latest prompt** (Glob V[LATEST]) — extract GEAR, SL, T1, active ARMs
3. **Prepare Context Brief**:
   ```
   Ticker: [SYMBOL]
   Current Price: $[LIVE_PRICE]
   Entry: $[ENTRY] | Change from entry: [+/-X%]
   SL: $[SL] | Distance to SL: [X%]
   T1: $[T1] | Distance to T1: [X%]
   GEAR: [X/5] | Active ARMs: [list]
   Context: [1-2 lines on what happened this week]
   ```

---

## PHASE 2 — BULL CAMP 🟢 (2-4 experts)

Select relevant experts from the HGEN Council based on the ticker:

### Neural Weights V274 (updated):
| Expert | Weight | Specialty |
|--------|--------|-----------|
| **Claude Sonnet 4.6 (Shannon)** | **1.52** | Information Theory, signal/noise |
| **Ray Dalio** | **1.49** | Global Macro, Store of Value |
| **Stan Druckenmiller** | 1.35 | Position Sizing, Macro Momentum |
| **Howard Marks** | 1.10 | Risk-adjusted, Credit cycles |
| **Nassim Taleb** | 1.15 | Black Swan, Antifragility |
| **Peter Lynch** | 1.00 | Growth at reasonable price |
| **Warren Buffett** | 1.05 | Value, moats, long-term |
| **George Soros** | **1.10** | Reflexivity, Energy wars |
| **Mandelbrot** | 1.25 | Tail risk ×1.5, Fat tails |

Each Bull expert presents:
1. Core argument (2-3 sentences)
2. Probability of positive outcome (%)
3. Supporting metric/evidence

---

## PHASE 3 — BEAR CAMP 🔴 (2-4 experts)

Select experts who naturally consider risks — Chanos, Taleb, Soros, Mandelbrot, Armstrong.

Each Bear expert presents:
1. Primary risk (2-3 sentences)
2. Loss scenario (% drop)
3. Mandelbrot ×1.5 tail risk estimate

---

## PHASE 4 — CROSS-EXAMINATION ⚔️

- Bull → Bear: challenges the weakest Bear point
- Bear → Bull: challenges the most dangerous Bull assumption
- Bull Response + Bear Response (1 sentence each)

---

## PHASE 5 — DA VINCI SYNTHESIS 🎨

**Truth synthesis**: Don't pick a side — **integrate**. Write 3-4 sentences combining the truth from both sides.

Apply:
- **Newton Humility**: Any probability > 85% — reduce to 85%
- **Mandelbrot ×1.5**: Any tail risk — multiply by 1.5
- **Zero-Loss Principle**: Does the proposed action endanger ZERO-LOSS principle?

---

## PHASE 6 — FINCON VERDICT ⚖️

```
## ⚖️ FINCON VERDICT: [TICKER]

| Parameter | Value |
|-----------|-------|
| **ACTION** | BUY / HOLD / TRIM / SELL / WAIT |
| **SIZE** | [shares] / [% of portfolio] |
| **ENTRY** | $[price] or MARKET |
| **SL** | $[STRICT_SL] |
| **T1** | $[target_1] (+X%) |
| **T2** | $[target_2] (+X%) |
| **Approval Level** | L1 (auto) / L2 (confirm) / L3 (HIGH-STAKES) |
| **HGEN Consensus** | X% Bull | Y% Bear | Z% Wait |
| **Newton Humility** | confidence capped: X% |
| **Mandate** | [one sentence — why this is the right move now] |
```

### Approval level definitions:
- **L1**: < $2,000 | Clear SL | GEAR ≥ 4 → immediate execution
- **L2**: $2,000-$20,000 | Requires confirmation | CONFIRM before trade
- **L3**: > $20,000 | HIGH-STAKES | meeting required

---

*URai SOVEREIGN PRIME V274+ | urai-hgen | HGEN Council 30 experts | Neural weights updated*
