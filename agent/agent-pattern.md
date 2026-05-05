# Agent Reasoning Pattern

> The complete reasoning chain. Each phase is discrete and auditable.

---

## Five-phase pipeline

```
Phase 1 — MONITOR    Fetch signals from configured sources
Phase 2 — FILTER     Remove irrelevant signals
Phase 3 — CLASSIFY   Assign tier, map to SportMind files
Phase 4 — REASON     Generate structured reasoning per item
Phase 5 — DELIVER    Format and dispatch the briefing
```

Each phase is stateless. Output can be inspected, resumed, or replayed independently.

---

## Phase 1 — MONITOR

Iterates through all enabled sources and fetches new content since `last_run`.

| Source type | Strategy |
|---|---|
| RSS feed | Parse feed, extract items after `last_run` |
| REST API | Call endpoint, extract relevant fields |
| Telegram public channel | Bot API `getUpdates` |
| GitHub API | Issues, releases, commits since `last_run` |

**Output:**
```json
{
  "source_id": "coindesk-regulation",
  "source_category": "regulatory",
  "title": "SEC Proposes Fan Token Guidance",
  "url": "https://coindesk.com/...",
  "published": "2026-05-04T14:32:00Z",
  "raw_text": "..."
}
```

**Error handling:** Source fetch failures are logged and skipped. Run continues. If >50% of sources fail, run aborts and sends alert. Rate limits respected: CoinGecko free tier = 10–30 calls/min, GitHub unauthenticated = 60/hour.

---

## Phase 2 — FILTER

Two-pass keyword filter per source category (see `sources/default-sources.md`).

- **Pass A — Inclusion:** at least one inclusion keyword must match
- **Pass B — Suppression:** signals matching suppression patterns are discarded even if they pass inclusion

Common suppression: routine price updates, match results, promotional content, duplicates within dedup window.

**Output:** Same structure as Phase 1 with added `filter_result` and `filter_reason`. Suppressed signals are logged for audit.

---

## Phase 3 — CLASSIFY

LLM step. Each filtered signal is passed with this prompt:

```
You are classifying a signal for the SportMind intelligence library.

SportMind covers: fan tokens on Chiliz Chain, sports analytics,
macro crypto, regulatory frameworks, athlete performance.

Tier 1: Confirmed, modifier-changing, actionable within 30 days
Tier 2: Credible, directionally consistent, adds specificity
Tier 3: Relevant, below Tier 2 threshold, worth monitoring

Signal:
TITLE: {title}
SOURCE: {source}
TEXT: {raw_text}

Respond in JSON:
{
  "tier": 1 | 2 | 3 | null,
  "tier_reason": "one sentence",
  "affects_files": ["path/to/file.md"],
  "affects_modifiers": ["modifier_id ×value"],
  "pending_mapping": true | false,
  "pending_reason": "if applicable"
}
```

The prompt receives SportMind context: full file tree, active modifiers, intake framework.

**Output:**
```json
{
  "signal_id": "T1-REG-20260505-001",
  "tier": 1,
  "tier_reason": "Confirmed SEC guidance, changes us_regulatory_clear modifier, actionable immediately",
  "affects_files": ["macro/sec-cftc-overview.md", "fan-token/regulatory-risk-layer.md"],
  "affects_modifiers": ["us_regulatory_clear ×1.15"],
  "pending_mapping": false
}
```

---

## Phase 4 — REASON

LLM step. Generates the full briefing item per classified signal.

```
You are generating a SportMind intelligence briefing item.
Signal classified as Tier {tier}.

TITLE: {title} | SOURCE: {source} | URL: {url} | TEXT: {raw_text}
AFFECTS FILES: {affects_files} | AFFECTS MODIFIERS: {affects_modifiers}

Generate:
SIGNAL: [2–4 sentences, factual only]
REASON TO ADD: [2–3 sentences against Tier criteria]
RECOMMENDED CHANGE: [Tier 1 only — name file, section, exact edit]
VALUE ADDED: [1–2 sentences on reasoning improvement]

Rules:
- SIGNAL is factual only, no editorial language
- RECOMMENDED CHANGE must name a specific file and section
- Do not invent modifier values
```

---

## Phase 5 — DELIVER

1. Sort: Tier 1 → Tier 2 → Tier 3 → Pending Mapping
2. Generate summary header
3. Build Tier 3 table and Agent Notes
4. Apply delivery formatting
5. Validate against checklist in `briefing/briefing-format.md`
6. Dispatch
7. Update `last_run`, add signal IDs to dedup store

---

## Configuration

```yaml
# agent/config.yml
agent:
  last_run: null
  llm_provider: anthropic        # anthropic | openai | local
  llm_model: claude-sonnet-4-20250514
  classification_temperature: 0.1
  reasoning_temperature: 0.3

sources:
  regulatory:       enabled: true
  chiliz:           enabled: true
  sports_calendar:  enabled: true
  macro_crypto:     enabled: true
  fan_token:        enabled: true

filters:
  min_tier: 2
  max_items_per_run: 12
  dedup_window_days: 7

delivery:
  method: github_issue
  github:
    owner: SportMind
    repo: SportMind
    token_env: SPORTMIND_GH_TOKEN
```

---

## Audit log

Every run produces `logs/YYYY-MM-DD.jsonl` containing all raw signals, filter decisions, classification results, delivered item IDs, and delivery status. Answers: "Why wasn't this signal in the briefing?"

---

## FETCH_ONLY mode

If no LLM is configured, phases 1 and 2 run and filtered signals are saved to `output/pending-classification.json` for manual classification. Completed items are passed to Phase 5 for delivery.

---

*Agent pattern v1.0.0 — SportMind/intelligence-agent*
