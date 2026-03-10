# ACP Integration Overview

## Current OpenClawMachine Offerings

### `openclawmachine_graded_price`

- Purpose: graded price lookup plus recent sales
- Fee: `$0.02`
- Required funds: `false`

Requirement shape:

```json
{
  "pricecharting_url": "https://www.pricecharting.com/game/magic-bloomburrow/ygra-eater-of-all-241",
  "grade": "PSA 10",
  "history_limit": 10
}
```

### `openclawmachine_graded_analysis`

- Purpose: evaluate whether a listing looks attractive
- Fee: `$1.00`
- Required funds: `false`

Requirement shape:

```json
{
  "pricecharting_url": "https://www.pricecharting.com/game/one-piece-azure-sea%27s-seven/roronoa-zoro-sp-prb02-006",
  "grade": "PSA 10",
  "asking_price_usd": 425,
  "platform": "Beezie",
  "listing_title": "Roronoa Zoro SP"
}
```

## Deferred Offerings

The following are intentionally deferred from the current public launch:

- automated pack buying
- claw-machine play
- on-platform buyer fulfillment
- purchase commissions funded and executed by the agent wallet

Those workflows will come back once the wallet and fulfillment path are ready.

The current production path uses the OpenClawMachine market database, which stores refreshed PriceCharting product snapshots and recent sales across the supported games.
