# FAQ

## What is live right now?

Database-backed graded price lookup and graded purchase analysis across supported TCG product pages.

## Is pack buying live?

**No.** Pack buying and public claw-machine play are disabled until escrow contracts are hardened, documented, and audited.

## Can users vault NFTs with OpenClawMachine?

**No for public product.** Do not send NFTs to a Phala/company vault for OpenClaw packs.  
Future packs use **on-chain escrow contracts** (Base for ERC-721s). Physical vaulting stays with issuers like Beezie or Collector Crypt.

## Solana or Base or Robinhood?

| Use | Chain |
| --- | --- |
| Analysis data | Off-chain (PriceCharting → D1) — chain-agnostic |
| NFT packs (planned) | **Base** |
| Platform token / USDG / stock packs (planned) | **Robinhood Chain** |
| Solana packs | **Deferred** |

## Are packs “provably fair”?

Planned contracts use **commit-reveal** with **uniform** selection over remaining inventory. That is not operator-picked. It is also not Chainlink VRF. See [narrative](narrative.md#randomness-honest-wording).

## Do you compete with Beezie / Collector Crypt?

Different layer. They vault **physical** cards and often stock their own gacha. OpenClaw targets **open contracts** on assets users already hold, plus analysis agents can call today.

## What inputs work best for analysis?

A direct PriceCharting product URL plus grade and asking price.

## Is the analysis a guarantee?

No. Informational comps and sale history only.

## Why reduce scope first?

Analysis can ship safely before autonomous buying, wallet execution, and pack fulfillment are production-ready.

## Where is the product narrative?

[Product Narrative](narrative.md) — single source of truth for live vs planned claims.
