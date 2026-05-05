# Changelog — SportMind/intelligence-agent

---

## [1.0.1] — 2026-05-05

### Fixed

- `README.md` — corrected suite position from "fifth" to "fourth"
- `CHANGELOG.md` — corrected suite position from "fifth" to "fourth"

---

## [1.0.0] — 2026-05-05

### Added

- `README.md` — repository overview, suite context, quick start (three options), delivery table, source categories, classification tiers, contributing pointer
- `sources/default-sources.md` — 28 curated public sources across 5 categories: Regulatory, Chiliz ecosystem, Sports calendar, Macro crypto, Fan token specific. All public, ToS-compliant, RSS/API-based. Per-category filter criteria defined.
- `classification/intake-framework.md` — Three-tier classification (Tier 1 Primary, Tier 2 Corroborating, Tier 3 Background Context), Gate 1/2/3 decision logic, PENDING_MAPPING as a first-class state, modifier mapping reference. Maps directly to `core/external-intelligence-intake.md` in SportMind/SportMind.
- `briefing/briefing-format.md` — Full item block specifications for Tier 1, Tier 2, Tier 3, and Pending Mapping. Signal ID format, formatting rules, GitHub Issue format, pre-delivery validation checklist.
- `briefing/delivery-options.md` — GitHub Issue (default), Telegram (push mode), Email digest. Full setup instructions per method. Combined delivery and dry-run support.
- `agent/agent-pattern.md` — Five-phase pipeline: MONITOR, FILTER, CLASSIFY, REASON, DELIVER. LLM prompt templates for classification and reasoning. Error handling, rate limit strategy, audit log specification, FETCH_ONLY mode.
- `agent/schedule-options.md` — Per-category cadence guidance, signal velocity reference, four use-case schedule templates, manual run CLI reference.
- `examples/sample-briefing.md` — Complete worked example: T1-REG (CFTC no-action letter), T2-CHZ (Socios LaLiga expansion), T2-FAN (BAR Copa del Rey win-burn), T3-MAC (BTC dominance monitoring).
- `examples/github-actions-workflow.yml` — Drop-in GitHub Actions workflow. Weekly full briefing + optional daily monitoring job. Manual trigger with inputs. Full secrets documentation.
- `CONTRIBUTING.md` — Ground rules, step-by-step for adding sources, extending classification, adding delivery options, submitting example briefings.
- `LICENSE` — MIT

### Architecture decisions

- **No external dependencies beyond `requests` and `python-dateutil`** — consistent with SportMind zero-dependency ethos
- **GitHub Issue as default delivery** — searchable, auditable public record, zero infrastructure beyond a PAT
- **PENDING_MAPPING as a first-class state** — unmapped signals surface library gaps rather than being silently discarded
- **LLM-agnostic prompt design** — works with any instruction-following model
- **Dedup window default of 7 days** — prevents repeat noise while allowing genuine new developments through

---

*SportMind/intelligence-agent — fourth repository in the SportMind suite*
