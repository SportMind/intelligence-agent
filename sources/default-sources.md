# Default Intelligence Sources

> Curated list of high-signal public sources organised by category.
> All sources are publicly accessible, RSS/API-based, and ToS-compliant.

---

## Category 1 — Regulatory

**ENABLED**

SportMind files affected: `macro/regulatory-frameworks.md`, `macro/sec-cftc-overview.md`, `macro/mica-implementation.md`, `fan-token/regulatory-risk-layer.md`

| Source | Feed / Endpoint | Signal type | Notes |
|---|---|---|---|
| CoinDesk — Regulation | `https://www.coindesk.com/arc/outbound/rss/regulation/` | RSS | High signal-to-noise on crypto regulation |
| SEC EDGAR full-text search | `https://efts.sec.gov/LATEST/search-index?q="fan+token"&dateRange=custom&startdt={LAST_RUN}` | REST (public) | Filings mentioning fan tokens |
| CFTC press releases | `https://www.cftc.gov/rss/pressreleases.xml` | RSS | Enforcement actions, no-action letters |
| ESMA | `https://www.esma.europa.eu/rss.xml` | RSS | MiCA implementation guidance |
| UK FCA | `https://www.fca.org.uk/news/rss.xml` | RSS | UK regulatory posture on crypto |
| Kaiko Research | `https://research.kaiko.com/rss` | RSS | Market structure analysis |

**Filter:** Pass if mentions `fan token`, `CHZ`, `Socios`, `Chiliz`, `MiCA`, `SEC enforcement`, `CFTC guidance`, or `retail crypto`. Suppress DeFi/NFT/stablecoin signals with no sports connection.

---

## Category 2 — Chiliz Ecosystem

**ENABLED**

SportMind files affected: `fan-token/chiliz-chain-infrastructure.md`, `fan-token/socios-platform-layer.md`, `macro/chiliz-ecosystem-overview.md`

| Source | Feed / Endpoint | Signal type | Notes |
|---|---|---|---|
| Chiliz official blog | `https://medium.com/feed/chiliz` | RSS | Protocol upgrades, partnerships |
| Socios.com blog | `https://medium.com/feed/socios` | RSS | Platform features, new clubs |
| Chiliz Chain explorer | `https://scan.chiliz.com/api?module=stats&action=tokensupply` | REST (public) | CHZ supply delta |
| CoinGecko — CHZ | `https://api.coingecko.com/api/v3/coins/chiliz?localization=false&tickers=false&market_data=true` | REST (free tier) | Price action, volume spikes |
| CoinGecko — Fan token list | `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&category=fan-token&order=market_cap_desc&per_page=50` | REST (free tier) | Full fan token market snapshot |
| Chiliz GitHub (public) | `https://api.github.com/repos/chiliz-chain/chz-chain/events` | REST (GitHub API) | Protocol code activity |
| Socios via Nitter | `https://nitter.net/socios/rss` | RSS | Real-time announcements |

**Filter:** Pass if signal represents new club partnership, governance vote, supply change, CHZ price move >15% in 24h, or protocol upgrade. Suppress routine price updates and promotional content.

---

## Category 3 — Sports Calendar

**ENABLED**

SportMind files affected: `market/competition-calendar.md`, `market/transfer-window-intelligence.md`, sport-specific files in `sports/`

| Source | Feed / Endpoint | Signal type | Notes |
|---|---|---|---|
| ESPN — UCL fixtures | `https://site.api.espn.com/apis/site/v2/sports/soccer/uefa.champions_league/scoreboard` | REST (public) | UCL schedule |
| ESPN — General sports | `https://www.espn.com/espn/rss/news` | RSS | Competition announcements |
| Transfermarkt | `https://www.transfermarkt.com/rss/transfers/news/0` | RSS | Transfer window activity |
| BBC Sport | `https://feeds.bbci.co.uk/sport/rss.xml` | RSS | Broad sports calendar |
| Formula 1 | `https://www.formula1.com/content/fom-website/en/latest/all.xml` | RSS | F1 calendar, qualifying |
| UEFA | `https://www.uefa.com/rssfeed/news.xml` | RSS | European competition schedules |
| FIFA | `https://www.fifa.com/rss/en/news.xml` | RSS | International calendar |

**Filter:** Pass if signal involves a club with an active fan token, opens/closes a transfer window, or creates a supply event trigger (title win, relegation, cup final). Suppress routine match results.

---

## Category 4 — Macro Crypto

**ENABLED**

SportMind files affected: `macro/crypto-cycle-framework.md`, `macro/market-structure-signals.md`, `fan-token/macro-modifier-layer.md`

| Source | Feed / Endpoint | Signal type | Notes |
|---|---|---|---|
| CoinDesk — Markets | `https://www.coindesk.com/arc/outbound/rss/markets/` | RSS | Macro crypto coverage |
| CoinGecko — Global | `https://api.coingecko.com/api/v3/global` | REST (free tier) | Market cap, BTC dominance |
| Glassnode Academy | `https://academy.glassnode.com/rss.xml` | RSS | On-chain cycle analysis |
| The Block | `https://www.theblock.co/rss/all` | RSS | Institutional flows |
| Bitcoin Magazine | `https://bitcoinmagazine.com/feed` | RSS | BTC cycle signals |
| Binance announcements | `https://www.binance.com/en/support/announcement/rss` | RSS | Exchange listings |
| Coinbase blog | `https://www.coinbase.com/blog/rss` | RSS | US institutional adoption |

**Filter:** Pass if signal indicates BTC entering a cycle phase, a fan token listed on a major exchange, market cap crossing a structural threshold, or institutional launch relevant to sports/fan tokens. Suppress altcoin signals with no fan token connection.

---

## Category 5 — Fan Token Specific

**ENABLED**

SportMind files affected: `fan-token/supply-event-calendar.md`, `fan-token/lifecycle-phases.md`, `fan-token/gamified-tokenomics.md`

| Source | Feed / Endpoint | Signal type | Notes |
|---|---|---|---|
| CoinGecko — Fan tokens (volume) | `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&category=fan-token&order=volume_desc&per_page=50` | REST (free tier) | Volume spike = likely supply event |
| Socios Telegram (public) | `https://api.telegram.org/bot{TOKEN}/getUpdates?chat_id=@sociosofficial` | Telegram Bot API | Platform announcements |
| Chiliz explorer — token events | `https://scan.chiliz.com/api?module=token&action=gettokeninfo&contractaddress={address}` | REST (public) | Per-token supply changes |
| CoinMarketCap — Fan tokens | `https://pro-api.coinmarketcap.com/v1/cryptocurrency/category?id=604f2573f13ebf1f6af3da2f` | REST (free tier key) | New fan token listings |
| SportMind/SportMind issues | `https://api.github.com/repos/SportMind/SportMind/issues?state=open&labels=supply-event` | REST (GitHub API) | Community-flagged supply events |
| Nitter — #FanToken | `https://nitter.net/search/rss?q=%23FanToken+%23Socios&f=tweets` | RSS | Social signals |

**Filter:** Pass if signal confirms a new token launch, records a supply event (burn or mint), announces a new exchange listing, or shows >25% volume spike with no price movement. Suppress routine updates.

---

## Source configuration

```yaml
# agent/config.yml
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
```

---

*Sources last audited: 2026-05-05 — SportMind/intelligence-agent v1.0.0*
