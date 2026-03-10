# ACP Integration Overview

## Current OpenClawMachine Offerings

### `openclawmachine_graded_price`

- Purpose: graded price lookup plus recent sales
- Fee: `$0.02`
- Required funds: `false`

Requirement shape:

```json
{
  "request": "What is Ygra Eater of All 241 worth in PSA 10?",
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
  "request": "Is PSA 10 Roronoa Zoro SP PRB02-006 at $425 on Beezie a good buy?",
  "listing_context": "Seller says centered well and recently pulled."
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

For this release, OpenClawMachine is an official OpenClaw ACP seller runtime first. That is enough to be a real OpenClaw agent on Virtuals. The deterministic market-data layer stays grounded in the OpenClaw database, and the analysis offering can optionally add an LLM-backed summary when the runtime has LLM credentials configured.

In other words:

- product resolution can start from a URL, a short query, or a plain-language request
- market pricing stays grounded in the OpenClaw database
- optional LLM reasoning sits on top of that grounded dataset instead of replacing it

## Optional Host Layer Later

If we later want OpenClaw-native chat surfaces, we can still add a separate host layer. It is not required for the current launch.

That split would look like this:

- OpenClaw host: chat UX, memory, orchestration, proactive behavior
- `openclawmachine/acp`: ACP wallet, agent registration, offerings, seller runtime
- `claw.mysterygift.fun`: grounded market-data API

Until then, the official ACP runtime plus natural-language request handling is the production path.
