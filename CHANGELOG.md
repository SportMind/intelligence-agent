# Changelog — SportMind/intelligence-agent

---

## [1.2.0] — 2026-05-06

### Fixed — website (index.html)

- Removed badge line (`Open source · MIT License · vX.X.X`) from hero section — version references belong in footer/changelog only
- Removed `Pele Roberts` from footer copyright — now reads `© 2026 SportMind`
- Added working mobile hamburger menu — drawer opens/closes with ☰/✕ toggle, closes on link click and outside click, aria-expanded state managed correctly
- All touch targets raised to 44px minimum — nav buttons, theme toggle, CTA buttons, footer links, suite links
- Added `overflow-x: hidden` to body — eliminates horizontal scroll on all viewports
- Added `overflow-x: auto` to `.bf-val` — briefing code fields scroll within container, no layout break
- Added 768px tablet breakpoint — delivery grid 2-column, pipeline grid adjusted, `.ww` padding corrected
- Added 480px small mobile breakpoint — suite cards stack to single column, buttons full-width, padding tightened
- All font sizes use `clamp()` — h1, h2, .sub, .prose, .stat-n scale correctly across all viewports
- Stats grid, suite cards, source cards, pipeline steps, briefing rows all collapse correctly on mobile
- Suite section correctly identified as Repository 04 (fourth in suite, not fifth)
- Footer wraps correctly on mobile with `flex-wrap: wrap`
- Nav links hidden on mobile with hamburger visible, GitHub link in drawer

### Fixed — repository files

- `CHANGELOG.md` — updated with v1.2.0 entry

### Verified correct (no change needed)

- All nav links present and working: How it works, Sources, Briefing format, GitHub ↗
- Logo links to sportmind.dev correctly
- Theme toggle present and functional (system/light/dark cycle)
- All footer links correct — GitHub, Changelog, Contribute, MIT License, sportmind.dev
- sportmind.dev link in footer points correctly
- All four suite repositories represented in suite section
- `Chiliz ecosystem` retained as source category name (refers to the Chiliz ecosystem, not SportMind suite — correct)
- GitHub Pages URL correct: `https://sportmind.github.io/intelligence-agent`
- `LICENSE` — MIT, standard attribution retained (industry convention for open source)

---

## [1.1.0] — 2026-05-05

### Added

- `index.html` — GitHub Pages site. Matches the design language of the SportMind suite (Geist/Geist Mono, identical CSS tokens, component patterns, theme toggle, scroll reveal). Sections: hero, stats bar, How it works (five-step pipeline), Sources (five category cards), Briefing format (worked example — all seven fields), Delivery options (GitHub Issue / Telegram / Email), SportMind Suite (four-column repository overview), CTA, footer.

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

---

*SportMind/intelligence-agent — fourth repository in the SportMind suite*
