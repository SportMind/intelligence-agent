# Contributing to intelligence-agent

---

## What can be contributed

| Contribution type | Effort | Impact |
|---|---|---|
| New source | Low | Expands signal coverage |
| Source filter tuning | Low | Improves signal-to-noise |
| Classification rule addition | Medium | Improves tier accuracy |
| New delivery option | Medium | Expands reach |
| Agent pattern improvement | High | Improves reasoning quality |
| New example briefing | Low | Improves documentation |

---

## Ground rules

1. **No paywalled sources** — every source must be publicly accessible without authentication beyond a free-tier API key
2. **No scraping** — use RSS feeds or official APIs only
3. **No ToS violations** — verify automated access is permitted for each source
4. **Every source must map to a SportMind file** — if you can't name one, the source isn't ready
5. **Test before submitting** — run the agent with your changes and include sample output in your PR

---

## Adding a new source

**Step 1 — Confirm:**
- [ ] Public RSS feed or free-tier API exists
- [ ] Automated access is ToS-compliant
- [ ] At least one SportMind file is clearly affected
- [ ] At least 1–2 relevant signals per month

**Step 2 — Add to `sources/default-sources.md`:**
```markdown
| Source name | Feed URL or API endpoint | Signal type | Notes |
```
Define inclusion keywords and suppression rules.

**Step 3 — Test:**
```bash
python agent/run.py --sources [category] --dry-run --verbose
```
Include captured signals (with filter results) in your PR description.

**Step 4 — PR:**
- Title: `feat(sources): add [Source Name] to [category]`
- Body: source URL, filter criteria, sample signals, SportMind file(s) affected

---

## Extending classification logic

Changes to `classification/intake-framework.md` affect every signal. Tier criteria changes require:
- A clear problem statement — what reasoning failure does this fix?
- Before/after examples — a signal misclassified before, correctly classified after
- Confirmation the change doesn't break existing correct classifications

If adding a new modifier type, verify it exists (or should exist) in `SportMind/SportMind` first.

---

## Adding a new delivery option

Requirements:
1. Zero additional infrastructure for default users
2. Secret-based credentials only
3. Must respect `--dry-run`
4. Full setup section added to `briefing/delivery-options.md`

Pattern:
```python
# agent/delivery/your_option.py
class YourOptionDelivery:
    def validate(self): ...
    def deliver(self, briefing: str, metadata: dict, dry_run: bool = False) -> bool: ...
```

---

## Submitting a new example briefing

Example briefings must:
- Follow `briefing/briefing-format.md` exactly
- Use real signals
- Include at least one Tier 1 item
- Name specific SportMind files and modifiers throughout

---

## Questions

Open an Issue in `SportMind/intelligence-agent` or in `SportMind/SportMind` tagged `intelligence-agent`.

---

*Contributing guide v1.0.0 — SportMind/intelligence-agent*
