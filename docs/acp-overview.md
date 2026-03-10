# ACP Integration Overview

## Current OpenClawMachine Offerings

### `openclawmachine_graded_price`

- Purpose: graded price lookup plus recent sales
- Fee: `$0.02`
- Required funds: `false`

Requirement shape:

```json
{
  "query": "Ygra Eater of All 241",
  "game": "magic",
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
  "query": "Roronoa Zoro SP PRB02-006",
  "game": "onepiece",
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

## Current Resource Surface

The current reduced launch should register only one ACP resource:

- `openclaw_market_data_api`
  - URL: `https://claw.mysterygift.fun/api/v1/market-data`
  - local ACP folder: `src/seller/resources/openclaw_market_api`
  - purpose: read-only graded price lookup and listing-analysis data

Do not register pack-catalog, commission, or gacha resources for this launch.

## Registration Runtime

The live OpenClawMachine seller runtime is maintained in `openclawmachine/acp`, checked out locally at:

- `/Users/area/repos/mystery-gift/virtuals-protocol-acp`

The older `openclawmachine/agent` scaffold is legacy only and should not be used for the current registry launch.

For this release, OpenClawMachine is an official OpenClaw ACP seller runtime first. The deterministic market-data layer stays grounded in the OpenClaw database, and the analysis offering can optionally add an LLM-backed summary when the runtime has LLM credentials configured.
