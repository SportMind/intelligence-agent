# Schedule Options

> Recommended monitoring cadence by source category.

---

## Default

```
Weekly — Monday 07:00 UTC
GitHub Actions cron: 0 7 * * 1
```

---

## Cadence by source category

| Category | Recommended cadence | Rationale |
|---|---|---|
| Regulatory | Weekly | Slow-moving. SEC/CFTC filings rarely require same-day response. |
| Chiliz ecosystem | Bi-weekly (Mon + Thu) | Partnerships can emerge mid-week. Thursday prevents a 6-day gap. |
| Sports calendar | Weekly | Transfer windows and schedules operate on known cycles. |
| Macro crypto | Daily (07:00 UTC) | Exchange listings and cycle signals can be time-sensitive. |
| Fan token specific | Daily (07:00 UTC) | Supply events are triggered by match outcomes — any day. |

---

## Multi-schedule configuration

```yaml
# agent/config.yml
schedules:
  full_briefing:
    cron: "0 7 * * 1"
    sources: all
    delivery: github_issue

  fan_token_daily:
    cron: "0 7 * * *"
    sources: [fan_token, macro_crypto]
    delivery: telegram
    tier_filter: 1
```

---

## Signal velocity reference

| Source | Signals/week (all) | Pass filter | Notes |
|---|---|---|---|
| CoinDesk regulation | 15–25 | 2–4 | Good filter pass rate |
| SEC EDGAR | 3–8 | 0–2 | Most weeks zero fan token filings |
| CFTC press releases | 1–3 | 0–1 | Slow but high value when active |
| Chiliz blog | 1–3 | 1–3 | Almost all relevant |
| CoinGecko fan tokens | 50–200 | 3–8 | Volume spikes are the signal |
| Socios Telegram | 5–15 | 2–5 | Promotional content filtered aggressively |
| Transfermarkt | 20–50 | 1–3 | Transfer window = 5–10× volume |
| Fan token supply events | 0–7 | 0–7 | Cup finals = peak |

**Expected per weekly run: 4–10 items (1–3 Tier 1, 2–4 Tier 2, 2–5 Tier 3)**

---

## Use case templates

**Library maintainer**
```
Full briefing:    Weekly, Monday 07:00 UTC
Fan token alerts: Daily, Tier 1 push only
Delivery:         GitHub Issue + Telegram
```

**Researcher / analyst**
```
Full briefing:    Weekly, Monday 07:00 UTC
Delivery:         Email digest
```

**Commercial operator**
```
Full briefing:    Bi-weekly, Mon + Thu 07:00 UTC
Fan token alerts: Daily, Tier 1 + Tier 2
Delivery:         Telegram + GitHub Issue
```

**Minimal / evaluation**
```
Full briefing:    Weekly, Monday 07:00 UTC
Sources:          Fan token + Regulatory only
Delivery:         Terminal
```

---

## Manual runs

```bash
python agent/run.py                          # full run
python agent/run.py --sources regulatory     # one category
python agent/run.py --since 2026-04-28       # catch up on missed signals
python agent/run.py --dry-run                # no delivery
```

---

*Schedule options v1.0.0 — SportMind/intelligence-agent*
