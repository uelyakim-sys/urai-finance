---
name: urai-laws-arm
description: >
  URai Laws & ARM Engine — loads all Laws and active ARMs from the latest prompt version,
  identifies which ARMs are triggered now based on live market data, and applies relevant Laws.
  Use for: 'which ARMs are active?', 'which laws apply?', 'is LAW_870 active?', ARM check,
  'what are the signals?', signal scan, 'what are the alerts?', risk rules check. Also runs
  automatically before HGEN and GEAR to ensure latest rules are loaded. Triggers on: ARM,
  LAW, law, signal, alert, risk rule, what laws apply, protocol, trigger check, update laws.
---

# URai Laws & ARM Engine — SOVEREIGN PRIME V274+

## Mission
1. **Load** all Laws and ARMs from the latest prompt version
2. **Activate** ARMs against live market data
3. **Report** all active ARMs + relevant Laws
4. **Update** after each nightly research run

---

## STEP 1 — Load Latest Prompt

Glob: /Downloads/המרכבה/URai_V*_SOVEREIGN_PRIME_OPTIMIZED.md
Read the file with the highest number (V274, V275, etc.)

Extract:
- All ARMs (ARM_01 through ARM_69+)
- All LAWs listed as "Priority: CRITICAL" or "Priority: HIGH"
- Updated neural weights
- Updated GEAR table

---

## STEP 2 — ARMs Catalog (V274)

### Critical ARMs (always check):

**ARM_53 — GIAP (Israel/Iran GPR)**
- Trigger: GPR >= 80/100
- Current (V274): 96/100 MAXIMUM
- Action: XLE, LMT, ESLT, EQT → MAX overweight
- Check: WebSearch "Iran Israel war [date]"

**ARM_54 — CFTC Silver Contrarian**
- Trigger: CFTC silver specs at multi-year LOW + physical demand high
- Current (V274): MAX ACTIVE
- Action: PAAS, AG, physical silver → ACCUMULATE

**ARM_62 — Clive Thompson COMEX**
- Trigger: COMEX silver coverage < 90M oz + drainage rate > 500K oz/day
- Current (V274): ACTIVE (86M oz, 785K oz/day)
- Action: Silver physical market crisis → ACCUMULATE miners

**ARM_64 — VIX Re-Spike**
- Trigger: VIX > 25 | Deactivate: VIX < 20 for 5 consecutive days
- Current (V274): ACTIVE (VIX 25.09)
- Action: Risk-off environment → defensive positions

**ARM_68 — Inflation-PM Paradox Detector**
- Conditions (3 of 4 required):
  [1] Gold down >5% in 48h — ✅
  [2] FOMC hawkish — ✅
  [3] VIX > 25 — ✅
  [4] Physical PM demand at records — ✅
- Current (V274): 4/4 ACTIVATED
- Action: CONTRARIAN BUY gold, silver, miners

**ARM_69 — Llama 4 Scout Monitor**
- Priority: LOW | Monitoring mode
- Action: Track for finance fine-tuning

---

## STEP 3 — Critical Laws Quick Reference (V274)

**LAW_810 — Druckenmiller Position Count**
Max: CORE <= 15 + SATELLITE <= 10 = 25 total
IF violated → identify which positions to close

**LAW_822 — EWEP (Extreme War Event Protocol)**
Trigger: Full-scale war with direct energy threats
Current: ACTIVE MAXIMUM | Action: XLE, LMT, ITA, Gold all MAX

**LAW_848 — Stagflation Maximum**
Trigger: Oil > $95 + CPI > 3% + Fed hawkish
Current (V274): ACTIVE | Action: Energy, gold, real assets over bonds/growth

**LAW_849 — COMEX Level 3**
Trigger: COMEX coverage < 100M oz
Current (V274): Level 3 (86M oz) | Level 4 threshold: < 60M oz
Action: Accelerate silver/gold accumulation

**LAW_864 — South Pars Protocol**
Trigger: Qatar/South Pars LNG infrastructure hit
Current (V274): ACTIVE (Ras Laffan indefinite shutdown)
Action: EQT, Cheniere, LNG exporters → MAX OVERWEIGHT

**LAW_870 — Energy War Protocol**
Trigger: Both sides target energy PRODUCTION (not just logistics)
Current (V274): ACTIVE (Israel struck South Pars, Iran retaliated)
Action: ALL energy positions → MAXIMUM OVERWEIGHT | Oil floor: $95 minimum

**LAW_871 — War-Inflation PM Paradox**
Trigger: Gold/silver crash >5% in 48h DURING war AND FOMC hawkish
Current (V274): ACTIVE
Action: CONTRARIAN BUY — paper market manipulation, physical demand real

**LAW_872 — Silver $70 Floor Defense**
Trigger: All 5 conditions met (silver <$70, COMEX <90M, deficit, China ban, dealers sold out)
Current (V274): ALL 5 CONDITIONS MET
Action: MAXIMUM ACCUMULATION ZONE $66-$72

---

## STEP 4 — Live ARM Check

For each active ARM, check one live data point:
- ARM_53: WebSearch "Iran Israel war today"
- ARM_64: FRED VIXCLS
- ARM_68: Alpha Vantage GLD + FRED VIXCLS
- LAW_870: WebSearch "Brent crude oil price today"
- LAW_872: WebSearch "silver price today COMEX"

---

## STEP 5 — Output Format

```
## 🔔 URai ARM & LAW Status — [DATE]
*Loaded from: V[N] | Checked: live data ✅*

### 🔴 CRITICAL (active now)
| ARM/LAW | Name | Live Data | Status | Action |
| ARM_53 | GIAP | Iran war day [N] | 96/100 🔴 | Defense/Energy MAX |
...

### 🟠 HIGH (active)
...

### 🟢 MONITORING (not active, watching)
...

### 📋 Law Actions Summary
1. [LAW_X]: [ACTION] → [TICKER LIST]
```

---

## Auto-Update Protocol

After each Nightly Research:
1. Read /Downloads/המרכבה/URai_V[LATEST]_SOVEREIGN_PRIME_OPTIMIZED.md
2. Identify new ARMs (ARM_N+1, ARM_N+2)
3. Identify new Laws (LAW_M+1, ...)
4. Update tables above
5. Publish updated neural weights

---

*URai SOVEREIGN PRIME V274+ | urai-laws-arm | 872 Laws | 69 ARMs | Auto-update after nightly research*
