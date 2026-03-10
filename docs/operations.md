# Operations

## Production Storage

- Market catalog and stored PriceCharting snapshots live in Cloudflare D1
- Production database name: `openclaw-machine-production`
- Public API worker: `openclaw-machine-api`
- Coverage status endpoint: `GET /api/v1/market-data/stats`
- Miss is a separate Phala app and keeps its own app-state database, but graded Pokemon market data is intended to flow through this OpenClawMachine market-data service rather than a second scraper
- OpenClawMachine D1 is the canonical graded-market cache for both agents

## Automated Scraping

OpenClawMachine now runs two production cron jobs on Cloudflare Workers:

- `*/30 * * * *`
  - incremental catalog sync
  - prioritizes unseen sets first, then the stalest known sets
  - walks additional set pages with PriceCharting cursor pagination up to the configured per-set budget
  - refreshes up to `120` of the oldest pending or stale product snapshots
- `17 3 * * *`
  - deeper daily sync
  - uses the same cursor-aware set crawling, but with a larger per-set budget
  - expands more sets per game and refreshes up to `240` stale product snapshots

Freshness policy:

- user-facing lookups can force a live refresh when cached data is missing or older than `24h`
- scheduled crawling is tuned for roughly `48h` full-catalog freshness at current catalog size
- responses expose `updated_on` so users can evaluate the exact age of the snapshot they received

These jobs update the same D1 catalog used by:

- `GET /api/v1/market-data/products`
- `GET /api/v1/market-data/lookup`
- `POST /api/v1/market-data/analyze`

User-facing freshness fields:

- `updated_on` is returned on product rows, lookup results, analysis results, and snapshots
- `last_scraped_at` remains available on product records and storage metadata

## Failure Recovery

- catalog sync now preserves existing scrape state instead of resetting already-completed products back to `pending`
- normal refresh attempts skip `hard_failed` products and respect `next_retry_at` for soft-failed products
- soft failures use exponential backoff starting at `15m` and capping at `12h`
- hard failures are reserved for structural problems such as invalid product URLs, unsupported product pages, or clear `404` / `410` responses
- responses and product records now expose:
  - `failure_class`
  - `failure_count`
  - `last_failure_at`
  - `next_retry_at`

Practical meaning:

- `soft` means the product should retry automatically later
- `hard` means the last failure looked structurally invalid and will stay out of the normal retry pool until a forced refresh or source fix

## Rate Limits

Public market-data routes are intentionally stricter than the general API:

- `/api/v1/market-data/products`: `30` requests per minute per IP
- `/api/v1/market-data/lookup`: `12` requests per minute per IP
- `/api/v1/market-data/lookup?force_refresh=true`: `2` requests per minute per IP
- `/api/v1/market-data/analyze`: `6` requests per minute per IP

General anonymous API traffic is still capped separately at `60` requests per minute per IP.

## Backups

Current protection layers:

- Cloudflare D1 Time Travel for rollback and short-retention recovery
- Cloudflare-managed infrastructure redundancy for the hosted database itself
- repo-level nightly backup automation that exports D1 and uploads dated artifacts into R2 together with the Phala-hosted SQLite backups for Miss and the Pokemon TCG API

Reference implementation:

- `scripts/backups/run-nightly-backup.mjs`
- `.github/workflows/nightly-backups.yml`

Remaining operator task:

- configure lifecycle retention on the R2 backup bucket
