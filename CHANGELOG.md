# Changelog — SportMind/intelligence-agent

---

## [1.2.0] — 2026-05-11

### Fixed

- `index.html` — skill files count updated from 456 to 617
- `index.html` — calibration records count updated from 126 to 129

### Verified correct (no change needed)

- Suite section: Repository 04 (fourth) ✓
- All four suite cards present with correct links ✓
- Footer: © 2026 SportMind — no name ✓
- No "ecosystem" in SportMind suite context — Chiliz ecosystem retained as source category name (refers to Chiliz product ecosystem, correct) ✓
- Version reference current ✓

---

## [1.1.1] — 2026-05-06

### Fixed — website (index.html)

- Removed badge line (`Open source · MIT License · vX.X.X`) from hero section
- Removed name from footer copyright — now reads `© 2026 SportMind`
- Added working mobile hamburger menu — drawer opens/closes with ☰/✕ toggle, aria-expanded managed
- All touch targets raised to 44px minimum
- Added `overflow-x: hidden` to body — no horizontal scroll on any viewport
- Added `overflow-x: auto` to briefing value fields — code scrolls within container
- Four responsive breakpoints: 1024px, 768px, 720px, 480px
- All font sizes use `clamp()` — h1, h2, .sub, .prose, .stat-n
- Stats, suite cards, pipeline steps, delivery grid all collapse correctly on mobile
- Buttons full-width and centred on small mobile
- Suite section: Repository 04 confirmed as fourth

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
- `sources/default-sources.md` — 28 curated public sources across 5 categories: Regulatory, Chiliz ecosystem, Sports calendar, Macro crypto, Fan token specific. All public, ToS-compliant, RSS/API-based.
- `classification/intake-framework.md` — Three-tier classification, Gate 1/2/3 decision logic, PENDING_MAPPING, modifier mapping reference.
- `briefing/briefing-format.md` — Full item block specifications for Tier 1, Tier 2, Tier 3, Pending Mapping. Signal ID format, GitHub Issue format, validation checklist.
- `briefing/delivery-options.md` — GitHub Issue (default), Telegram (push mode), Email digest.
- `agent/agent-pattern.md` — Five-phase pipeline with LLM prompt templates, error handling, audit log, FETCH_ONLY mode.
- `agent/schedule-options.md` — Per-category cadence, signal velocity reference, four use-case templates.
- `examples/sample-briefing.md` — Complete worked example across four signal tiers.
- `examples/github-actions-workflow.yml` — Drop-in GitHub Actions workflow.
- `CONTRIBUTING.md` — Ground rules, step-by-step contribution guide.
- `LICENSE` — MIT

---

*SportMind/intelligence-agent — fourth repository in the SportMind suite*
