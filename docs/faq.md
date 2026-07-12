# FAQ

## What is live right now?

Database-backed graded price lookup and graded purchase analysis across supported TCG product pages.

## Is pack buying live?

**No.** Pack buying and public claw-machine play are disabled until escrow contracts are hardened, documented, and audited.

## Can users vault NFTs with OpenClawMachine?

**No for public product.** Do not send NFTs to a Phala/company vault for OpenClaw packs.  
Packs use **on-chain escrow contracts** (Base ERC-721, Robinhood ERC-20). The **TEE vault wallet is not required** for public packs — see [Vault Lifecycle](vault-lifecycle.md). Physical vaulting stays with issuers like Beezie or Collector Crypt.

## Solana or Base or Robinhood?

| Use | Chain |
| --- | --- |
| Analysis data | Off-chain (PriceCharting → D1) — chain-agnostic |
| NFT packs (Pokemon, One Piece, Beezie-class) | **Base** |
| Equity packs + AI/meme token packs + USDG | **Robinhood Chain** |
| Solana packs | **Deferred** |

## Are packs “provably fair”?

**Preferred:** Phala **Flash VRF** (TEE-signed on-chain request/fulfill) with uniform selection over reserved remaining inventory. Trust root includes the Phala TEE — not classical Chainlink ECVRF.  
**Fallback:** buyer **commit-reveal**.  
Chainlink VRF is optional on Base only; **not on Robinhood**. See [Randomness Architecture](randomness-architecture.md).

## Do we still need the TEE vault wallet app?

**Not for public packs.** Escrow contracts hold inventory. Keep the vault CVM only while Mystery Gift livestream / company-stock paths still transfer from a hot wallet. Details: [Vault Lifecycle](vault-lifecycle.md).

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
