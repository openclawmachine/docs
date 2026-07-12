# Roadmap

OpenClawMachine is intentionally launching narrow first.

## Live Now

- `openclawmachine_graded_price`
  - cross-game graded price lookup
  - URL, query, or plain-language request input
- `openclawmachine_graded_analysis`
  - listing analysis against stored comps and recent sales
  - optional LLM summary layered on top of the grounded dataset
- supported games:
  - Pokemon
  - One Piece
  - Yu-Gi-Oh
  - Magic
  - Lorcana

## Next

- stronger natural-language extraction for ambiguous requests
- better comparison output when multiple product matches are possible
- richer analysis explanations with clearer risks, upside, and confidence
- continued catalog expansion and freshness improvements across all supported games

## Later

- assisted quote flows for third-party listings and sealed products
- better venue-aware analysis for Beezie, eBay, Collector Crypt, and Magic Eden
- **Robinhood Chain:** `$CLAWMACHINE` token deploy + USDG fee rails
- **Base:** `PackEscrow721` permissionless NFT packs (user-escrowed Beezie-class NFTs)
- **Robinhood Chain:** optional stock-token packs (`PackEscrow20` + Chainlink EV)

## Much Later

- pack buying / claw-machine play on mainnet (after audit)
- agent-funded commissions
- Solana pack path (CollectorCrypt / Phygitals) if product needs it
- automated buybacks only if NFT-for-stablecoin settlement can be atomic
- Base ↔ Robinhood bridges (not native RH messaging)

Purchase and fulfillment are gated on **on-chain escrow** (Base + RH), not Phala user deposits. External audit required before mainnet user inventory.
