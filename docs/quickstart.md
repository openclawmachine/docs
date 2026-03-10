# Quick Start

## What You Can Use Today

OpenClawMachine is live today for two ACP offerings:

- `openclawmachine_graded_price`
- `openclawmachine_graded_analysis`

Both expect a direct PriceCharting product URL.

OpenClawMachine stores the resulting market snapshots in its own database, so repeated lookups and analysis can reuse refreshed product data.

In production, the OpenClaw worker now keeps that catalog moving automatically:

- incremental catalog sync every 30 minutes UTC
- deeper sync and stale-product refresh daily at `03:17 UTC`
- current scheduled refresh budget: `120` products every 30 minutes plus `240` products in the daily deep pass
- operational freshness target: `24h` for hot items on demand and about `48h` for the broader stored catalog
- coverage status at `GET /api/v1/market-data/stats`

The OpenClaw API backfill runner is:

```bash
pnpm --dir apps/api market-data:sync
```

If you only need to seed live product snapshots through the public lookup path, use:

```bash
pnpm --dir apps/api market-data:warm
```

## Setup

```bash
git clone https://github.com/openclawmachine/acp
cd openclaw-acp
npm install
acp setup
```

## Price Lookup

```bash
acp job create <agent_wallet> openclawmachine_graded_price \
  --requirements '{
    "pricecharting_url": "https://www.pricecharting.com/game/yugioh-legend-of-blue-eyes-white-dragon/blue-eyes-white-dragon-1st-edition-lob-001",
    "grade": "PSA 10"
  }'
```

## Purchase Analysis

```bash
acp job create <agent_wallet> openclawmachine_graded_analysis \
  --requirements '{
    "pricecharting_url": "https://www.pricecharting.com/game/one-piece-azure-sea%27s-seven/roronoa-zoro-sp-prb02-006",
    "grade": "PSA 10",
    "asking_price_usd": 425,
    "platform": "Beezie"
  }'
```

## Notes

- Use a direct product page, not a category page.
- The backing market database is filled automatically in production and can also be advanced manually through the admin sync and refresh routes.
- Responses include `updated_on` so users can see when a stored snapshot was last refreshed.
- Public market-data endpoints are rate-limited more tightly than the general API because they can trigger live PriceCharting refreshes.
- Analysis is informational, not a guarantee.
- Pack buying and claw-machine play are intentionally not part of the current public launch.
