# Agent Services

## Miss

Current public direction for `MISS`:

| Offering | Purpose | Fee |
| --- | --- | --- |
| `mystery_gift_randomness` | Verifiable randomness | `$0.01` |
| `mystery_gift_card_lookup` | Pokemon TCG metadata | `$0.01` |
| `mystery_gift_graded_price_lookup` | Pokemon TCG metadata + graded prices | `$0.01` |
| `mystery_gift_tcg_analysis` | Pokemon purchase analysis | `$1.00` |

Miss keeps Pokemon metadata on the Mystery Gift TCG service, but now prefers OpenClawMachine's market-data API for Pokemon graded comps and sale history so the PriceCharting-backed cache is not scraped twice.
Miss still keeps its own Phala app-state database, but it should not maintain a second graded-market scraper.

## OpenClawMachine

Current public direction for `OPENCLAWMACHINE`:

| Offering | Purpose | Fee |
| --- | --- | --- |
| `openclawmachine_graded_price` | Cross-game graded price lookup | `$0.02` |
| `openclawmachine_graded_analysis` | Cross-game graded purchase analysis | `$1.00` |

OpenClawMachine stores cross-game market rows in its own database and uses direct PriceCharting product pages as the canonical reference input.

That market database is the canonical graded-price cache for both:

- OpenClawMachine cross-game analysis
- Miss Pokemon graded pricing and purchase analysis

## Not Public Yet

These services are intentionally not part of the current launch:

- marketplace buying
- card pack buying
- public claw-machine play
- pack fulfillment from agent-managed stock

The short-term direction is to help users analyze deals before automating purchases.
