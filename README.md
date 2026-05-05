# intelligence-agent

> The fifth repository in the SportMind suite. Monitors, classifies, and delivers structured intelligence briefings. You decide what enters the library.

---

## What this is

A standalone, forkable briefing system that watches defined public sources on a schedule, classifies findings against the SportMind three-tier intake framework, and delivers a structured intelligence briefing with full reasoning.

It does not push to GitHub autonomously. It does not modify the library. It researches, classifies, and presents. **You decide what gets added.**

Every briefing item is mapped to a specific SportMind file and modifier. Signals with no clear library mapping are filtered before delivery. What reaches you is actionable, not noise.

---

## The SportMind suite

| Repository | Role |
|---|---|
| [SportMind/SportMind](https://github.com/SportMind/SportMind) | Core library — the intelligence primitive set |
| SportMind/mcp-server | MCP server — exposes library to AI agent runtimes |
| SportMind/agent-examples | Reference agent implementations |
| SportMind/calibration-registry | Public calibration record archive |
| **SportMind/intelligence-agent** | **This repository — monitoring, classification, briefing** |

---

## How it works

```
Monitor sources → Filter noise → Classify (Tier 1/2/3) → Map to SportMind files → Reason → Deliver briefing
```

1. **Monitor** — watches public RSS feeds, free-tier APIs, and public channels across five source categories
2. **Filter** — discards signals with no clear SportMind file mapping
3. **Classify** — assigns Tier 1, 2, or 3 using the intake framework
4. **Map** — identifies which specific SportMind files and modifiers are affected
5. **Reason** — generates a structured reasoning chain for each item
6. **Deliver** — opens a GitHub Issue in `SportMind/SportMind` titled `SportMind Intelligence Briefing — [date]`

See [`agent/agent-pattern.md`](agent/agent-pattern.md) for the full reasoning chain.

---

## Quick start

### Option A — GitHub Actions (recommended, zero cost on public repos)

1. Fork this repository
2. Add your GitHub token as a repository secret: `SPORTMIND_GH_TOKEN`
3. Edit [`sources/default-sources.md`](sources/default-sources.md) to enable/disable source categories
4. The workflow in [`examples/github-actions-workflow.yml`](examples/github-actions-workflow.yml) runs automatically on schedule

The default schedule is **weekly on Monday at 07:00 UTC**.

### Option B — Run locally

```bash
git clone https://github.com/SportMind/intelligence-agent
cd intelligence-agent

python agent/run.py --output terminal
```

### Option C — LLM-agnostic

The briefing format and classification framework are structured markdown. Load them into any agent runtime alongside the SportMind core library. See [`briefing/briefing-format.md`](briefing/briefing-format.md).

---

## Delivery options

| Method | Best for | Setup |
|---|---|---|
| GitHub Issue | Auditable public record (default) | Add `SPORTMIND_GH_TOKEN` secret |
| Telegram | Real-time mobile alerts | Add `TELEGRAM_BOT_TOKEN` + `TELEGRAM_CHAT_ID` |
| Email digest | Weekly summaries | Add SMTP credentials |

Full setup: [`briefing/delivery-options.md`](briefing/delivery-options.md)

---

## Source categories

- **Regulatory** — SEC/CFTC filings, MiCA updates, CoinDesk regulatory coverage
- **Chiliz ecosystem** — Socios announcements, CHZ on-chain data, fan token governance
- **Sports calendar** — competition schedules, transfer windows, fixture announcements
- **Macro crypto** — Bitcoin cycle signals, exchange listings, market structure events
- **Fan token specific** — new launches, supply events, burn/mint confirmations

Full source list: [`sources/default-sources.md`](sources/default-sources.md)

---

## Classification tiers

| Tier | Name | Action |
|---|---|---|
| Tier 1 | Primary signal | Immediate library update candidate |
| Tier 2 | Corroborating signal | Strengthens existing intelligence |
| Tier 3 | Background context | Monitoring only, no immediate action |

Full framework: [`classification/intake-framework.md`](classification/intake-framework.md)

---

## What a briefing looks like

See [`examples/sample-briefing.md`](examples/sample-briefing.md) for a complete worked example.

---

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## Compatibility

- Works alongside all four other SportMind suite repositories
- No external dependencies beyond Python standard library + `requests`
- Compatible with any LLM
- Classification framework maps directly to `core/external-intelligence-intake.md` in `SportMind/SportMind`

---

## License

MIT — see [`LICENSE`](LICENSE)

---

*SportMind/intelligence-agent v1.0.0*
