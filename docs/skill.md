# OpenClawMachine Skill

OpenClawMachine is currently a cross-game analysis agent, not a public buying or gacha-play agent.

## Live Today

- graded price lookup from stored market data
- graded purchase analysis against an asking price
- plain-language request handling through the OpenClaw ACP runtime
- support for Pokemon, One Piece, Yu-Gi-Oh, Magic, and Lorcana product pages from PriceCharting

## Not Public Yet

- pack buying
- claw-machine play
- agent-funded purchase commissions
- autonomous fulfillment

## Base URL

- site: `https://openclawmachine.xyz`
- API: `https://claw.mysterygift.fun/api/v1`

## Public Offerings

### `openclawmachine_graded_price`

- fee: `$0.02`
- input:

```json
{
  "request": "What is PSA 10 Blue-Eyes White Dragon 1st Edition worth?",
  "history_limit": 10
}
```

or

```json
{
  "query": "Blue-Eyes White Dragon 1st Edition",
  "game": "yugioh",
  "grade": "PSA 10"
}
```

### `openclawmachine_graded_analysis`

- fee: `$1.00`
- input:

```json
{
  "request": "Is PSA 10 Roronoa Zoro SP PRB02-006 at $425 on Beezie a good buy?"
}
```

## API Surface

### Search stored products

```http
GET /api/v1/market-data/products?q=blue-eyes&game=yugioh&limit=20
```

### Read coverage stats

```http
GET /api/v1/market-data/stats
```

### Lookup a stored snapshot

```http
GET /api/v1/market-data/lookup?pricecharting_url=https://www.pricecharting.com/game/magic-bloomburrow/ygra-eater-of-all-241&grade=PSA%2010
```

### Analyze a listing

```http
POST /api/v1/market-data/analyze
Content-Type: application/json

{
  "pricecharting_url": "https://www.pricecharting.com/game/magic-bloomburrow/ygra-eater-of-all-241",
  "grade": "PSA 10",
  "asking_price_usd": 85,
  "platform": "eBay"
}
```

## Data Pipeline

- production worker runs automatic catalog sync and snapshot refresh on Cloudflare cron
- market rows and recent sales are stored in Cloudflare D1
- direct product lookups can still trigger live refreshes when data is stale or missing
- current production refresh budget is `120` products every 30 minutes plus `240` in the daily deep pass
- operational freshness target is `24h` for hot items and roughly `48h` for the full stored catalog at current scale
- responses include `updated_on` so users can see when the stored market snapshot was last refreshed

## Rate Limits

- `/market-data/products`: `30` requests per minute per IP
- `/market-data/lookup`: `12` requests per minute per IP
- `/market-data/lookup?force_refresh=true`: `2` requests per minute per IP
- `/market-data/analyze`: `6` requests per minute per IP

## Launch Direction

Use OpenClawMachine to compare graded listings first. Revisit assisted buying and pack execution only after wallet safety, funding, and fulfillment controls are ready.

See [Roadmap](roadmap.md) for the planned service expansion path.
