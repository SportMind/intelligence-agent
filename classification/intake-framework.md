# Intelligence Intake Framework

> The classification system used by SportMind/intelligence-agent to evaluate, tier, and route incoming signals.
> Maps directly to `core/external-intelligence-intake.md` in SportMind/SportMind.

---

## Three gates

Every signal passes through three sequential gates before reaching the briefing:

```
Gate 1 — Relevance     Does this connect to a SportMind file or modifier?
Gate 2 — Tier          How actionable is this signal right now?
Gate 3 — Mapping       Can we name the exact SportMind file(s) affected?
```

Fail Gate 1 → discard. Pass Gate 1, fail Gate 3 → PENDING_MAPPING queue.

---

## Tier 1 — Primary Signal

**Definition:** A confirmed, material change to an external condition that directly modifies the validity or calibration weight of one or more SportMind modifiers.

**All three criteria must be met:**

1. **Confirmed, not rumoured** — from an official source, or confirmed by two independent Tier 2 sources
2. **Materially changes a modifier** — would cause a numeric change to a weight, threshold, or directional bias in a named SportMind file
3. **Actionable within 30 days** — the condition has already changed or will change within the current operational horizon

**Examples:**
- US SEC issues guidance classifying fan tokens as non-securities → `macro/sec-cftc-overview.md`, modifier: `us_regulatory_clear ×1.15`
- Socios confirms win-burn mechanic for a specific club → `fan-token/gamified-tokenomics.md`, modifier: `win_burn_confirmed ×1.20`
- Fan token listed on Coinbase → `fan-token/lifecycle-phases.md`, modifier: `major_exchange_listing ×1.10`

**Briefing action:** Always included with full reasoning and a specific `RECOMMENDED CHANGE` field.

---

## Tier 2 — Corroborating Signal

**Definition:** Credible, relevant, and directionally consistent with known SportMind intelligence — but does not independently justify a library change.

**At least two criteria must be met:**

1. Relevant to a known modifier
2. Directionally consistent with current library position
3. From a credible source (not speculation or social sentiment)
4. Adds specificity — a date, number, or named entity that adds resolution

**Examples:**
- Second analyst report confirming US fan token regulatory momentum
- Transfer window opening for a league with multiple fan token clubs
- CHZ on-chain volume up 40% week-on-week during a cup final run
- Bitcoin dominance drops below 50%

**Briefing action:** Included with a `CORROBORATES` field. No library change recommended unless two Tier 2 signals cover the same modifier.

---

## Tier 3 — Background Context

**Definition:** A relevant development that may become material in the future but does not currently justify a library change.

**Criteria:**
- Connected to a SportMind domain
- Does not meet Tier 1 or Tier 2 threshold
- Worth monitoring over 30–90 days

**Examples:**
- Sports federation considering tokenised fan engagement (rumour stage)
- New jurisdiction beginning a crypto asset consultation
- Club with no fan token announcing an NFT partnership

**Briefing action:** Summary table only. No `RECOMMENDED CHANGE`. Logged to `MONITORING_QUEUE`.

---

## PENDING_MAPPING

When a signal passes Gate 1 but Gate 3 fails (no SportMind file can be named), it enters `PENDING_MAPPING`. This signals either a library gap or an early-stage signal.

`PENDING_MAPPING` items appear in the briefing under their own section — they are a prompt for library expansion, not a failure.

---

## Decision tree

```
Incoming signal
       │
       ▼
┌─────────────────────────────────────────────┐
│ Gate 1: Does this connect to a SportMind    │
│ domain? (sports, fan tokens, crypto, macro) │
└─────────────────────────────────────────────┘
       │ NO → DISCARD
       │ YES
       ▼
┌─────────────────────────────────────────────┐
│ Gate 2: Tier classification                  │
│                                             │
│ Confirmed + modifier-changing + actionable? │
│   → Tier 1                                  │
│                                             │
│ Credible + consistent + specific (2+ met)?  │
│   → Tier 2                                  │
│                                             │
│ Relevant but below Tier 2?                  │
│   → Tier 3                                  │
└─────────────────────────────────────────────┘
       │
       ▼
┌─────────────────────────────────────────────┐
│ Gate 3: Can you name the SportMind file(s)? │
└─────────────────────────────────────────────┘
       │ NO → PENDING_MAPPING
       │ YES → INCLUDE IN BRIEFING
```

---

## Modifier mapping reference

| Modifier type | Example identifier | Affected layer |
|---|---|---|
| Athlete composite | `athlete_modifier ×1.10` | `athlete/` |
| Fan token supply event | `win_burn_confirmed ×1.20` | `fan-token/` |
| Macro environment | `crypto_cycle_bull ×1.08` | `macro/` |
| Regulatory risk | `us_regulatory_clear ×1.15` | `macro/`, `fan-token/` |
| Market depth | `major_exchange_listing ×1.10` | `market/`, `fan-token/` |
| Sport-specific | `dew_factor ×0.85`, `qualifying_delta ×1.12` | `sports/` |
| Geopolitical | `india_pakistan ×2.00` | `sports/`, `macro/` |

---

*Classification framework v1.0.0 — SportMind/intelligence-agent*
