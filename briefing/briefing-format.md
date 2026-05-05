# Briefing Format

> The standard format for every intelligence briefing item.
> Tier 1 requires all fields. Tier 2 and Tier 3 have reduced requirements as noted.

---

## Document structure

```
SportMind Intelligence Briefing — [ISO DATE]
Generated: [TIMESTAMP UTC]
Run type: [SCHEDULED | MANUAL]
Sources checked: [N] · Signals captured: [N] · Signals filtered: [N] · Items: [N]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Tier 1 — Primary Signals  ([N] items)
[ITEM BLOCKS]

## Tier 2 — Corroborating Signals  ([N] items)
[ITEM BLOCKS]

## Tier 3 — Background Context  ([N] items)
[SUMMARY TABLE]

## Pending Mapping  ([N] items)
[PENDING BLOCKS]

## Agent notes
[SUPPRESSION SUMMARY]
```

---

## Tier 1 item block

```markdown
### [SIGNAL_ID] — [SIGNAL TITLE]

**SOURCE**
[Publication / API / Channel]
[URL]
[Published timestamp UTC]

**SIGNAL**
[2–4 sentences — factual only, no interpretation]

**TIER**
Tier 1 — Primary Signal

**AFFECTS**
- File: `[exact SportMind file path]`
- Modifier: `[identifier ×value]`

**REASON TO ADD**
[2–3 sentences referencing the Tier 1 criteria — confirmed, modifier-changing, actionable within 30 days]

**RECOMMENDED CHANGE**
[Specific edit — name the file, section, and exact change]

**VALUE ADDED**
[1–2 sentences on how this improves agent reasoning accuracy]
```

---

## Tier 2 item block

```markdown
### [SIGNAL_ID] — [SIGNAL TITLE]

**SOURCE**
[Publication / API / Channel]
[URL]
[Published timestamp UTC]

**SIGNAL**
[2–3 sentences — factual only]

**TIER**
Tier 2 — Corroborating Signal

**AFFECTS**
- File: `[SportMind file path]`
- Modifier: `[identifier]`

**CORROBORATES**
[Name the existing SportMind file and section this strengthens]

**VALUE ADDED**
[1 sentence]
```

---

## Tier 3 summary table

```markdown
| ID | Signal | Source | Relevant file | Monitor until |
|---|---|---|---|---|
| T3-001 | [Brief title] | [Source] | [File] | [Date] |
```

---

## Pending Mapping block

```markdown
### [SIGNAL_ID] — PENDING MAPPING — [TITLE]

**SOURCE** / **SIGNAL** — as above

**WHY UNMAPPED**
[Library gap? New domain? Too early?]

**SUGGESTED ACTION**
[New file needed | Existing file needs expanding | Monitor 30 days | Discard]
```

---

## Signal ID format

```
[TIER]-[CATEGORY]-[DATE]-[SEQUENCE]

T1-REG-20260505-001   Tier 1, Regulatory
T2-CHZ-20260505-001   Tier 2, Chiliz
T3-MAC-20260505-001   Tier 3, Macro
PM-FAN-20260505-001   Pending Mapping, Fan Token
```

Category codes: `REG` `CHZ` `CAL` `MAC` `FAN`

---

## Formatting rules

1. Every briefing is valid Markdown
2. Every source has a URL — every signal is traceable
3. File paths in backticks — `fan-token/gamified-tokenomics.md`
4. Modifier values use × prefix — `win_burn_confirmed ×1.20`
5. Dates ISO 8601 — `2026-05-05`, timestamps UTC
6. SIGNAL field is factual only — no editorial language
7. RECOMMENDED CHANGE names a specific file and section — no vague language

---

## GitHub Issue format

Title: `SportMind Intelligence Briefing — 2026-05-05`
Labels: `intelligence-briefing`, `automated`, `tier-1` (if applicable)

Issue body opens with:

```markdown
> **Automated briefing** · [N] items · [N] Tier 1 · [N] Tier 2 · [N] Tier 3
> Sources checked: [N] · Run: [timestamp]
> Tier 1 signals require review. Close this issue when actioned.
```

---

## Pre-delivery validation checklist

- [ ] Every Tier 1 item has a named SportMind file in AFFECTS
- [ ] Every Tier 1 item has a specific RECOMMENDED CHANGE
- [ ] Every source has a URL
- [ ] No signal duplicated within the dedup window (default 7 days)
- [ ] No signal ID repeated in this briefing
- [ ] Tier 3 table has no more than 10 rows

---

*Briefing format v1.0.0 — SportMind/intelligence-agent*
