# Delivery Options

> Three delivery methods. Default is GitHub Issue — auditable, searchable, zero additional infrastructure.

---

## Option 1 — GitHub Issue (default)

Opens an Issue in `SportMind/SportMind` titled `SportMind Intelligence Briefing — [date]`.
Labels: `intelligence-briefing`, `automated`, `tier-1` if applicable.
The full briefing is the Issue body in Markdown. Close when actioned.

### Setup

1. Go to GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens
2. Set repository to `SportMind/SportMind`, permission: Issues — Read and write
3. In `SportMind/intelligence-agent`: Settings → Secrets and variables → Actions → New secret

```
Name:  SPORTMIND_GH_TOKEN
Value: [your token]
```

4. In `agent/config.yml`:

```yaml
delivery:
  method: github_issue
  github:
    owner: SportMind
    repo: SportMind
    token_env: SPORTMIND_GH_TOKEN
```

5. Test: `python agent/run.py --output github-issue --dry-run`

Search all past briefings: `is:issue label:intelligence-briefing repo:SportMind/SportMind`

---

## Option 2 — Telegram

Sends formatted Markdown messages to a private channel or group. Tier 1 signals can be delivered immediately (push mode) rather than waiting for the scheduled run.

### Setup

1. Open Telegram → `@BotFather` → `/newbot` → save the bot token
2. Create a private channel, add your bot as admin with posting rights
3. Get your chat ID: `curl "https://api.telegram.org/bot{TOKEN}/getUpdates"` — look for `chat.id`
4. Add secrets:

```
TELEGRAM_BOT_TOKEN  = [your bot token]
TELEGRAM_CHAT_ID    = [your chat id — negative number for groups/channels]
```

5. In `agent/config.yml`:

```yaml
delivery:
  method: telegram
  telegram:
    bot_token_env: TELEGRAM_BOT_TOKEN
    chat_id_env: TELEGRAM_CHAT_ID
    push_tier1: true
    full_briefing: true
```

### Tier 1 push alert format

```
🔴 *SportMind — Tier 1 Signal*

*T1-REG-20260505-001 — [Title]*

[Signal description]

*Affects:* `macro/sec-cftc-overview.md`
*Modifier:* `us_regulatory_clear ×1.15`

Full briefing: [Issue link]
```

---

## Option 3 — Email Digest

Sends an HTML email on schedule. Tier 1 signals are highlighted. Good for non-technical stakeholders.

### Setup

1. For Gmail: enable 2FA → Account → Security → App passwords → Generate a 16-character password
2. Add secrets:

```
SMTP_HOST      = smtp.gmail.com
SMTP_PORT      = 587
SMTP_USER      = your@gmail.com
SMTP_PASSWORD  = [16-character app password]
EMAIL_FROM     = SportMind Agent <your@gmail.com>
EMAIL_TO       = you@yourdomain.com
```

3. In `agent/config.yml`:

```yaml
delivery:
  method: email
  email:
    smtp_host_env: SMTP_HOST
    smtp_port_env: SMTP_PORT
    smtp_user_env: SMTP_USER
    smtp_password_env: SMTP_PASSWORD
    from_env: EMAIL_FROM
    to_env: EMAIL_TO
    subject_prefix: "SportMind Intelligence —"
    include_tier3: false
```

Subject format: `SportMind Intelligence — 2026-05-05 · 2 Tier 1 · 3 Tier 2`

---

## Combining methods

```yaml
delivery:
  methods:
    - github_issue   # full briefing, always
    - telegram       # Tier 1 push alerts only
```

---

## Terminal output

```bash
python agent/run.py --output terminal
```

No secrets required. Default when no delivery is configured.

---

## Dry run

```bash
python agent/run.py --output github-issue --dry-run
python agent/run.py --output telegram --dry-run
python agent/run.py --output email --dry-run
```

Renders the full briefing to terminal without making any external requests.

---

*Delivery options v1.0.0 — SportMind/intelligence-agent*
