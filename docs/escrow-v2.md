# Escrow V2 (Base + Robinhood Chain)

OpenClawMachine alpha is analysis-first. Public users must **not** deposit NFTs into a Phala/company service wallet.

## Current Policy

- Live product: graded prices, recent sales, listing analysis, market-data catalog.
- Phala vault signing is a **company hot wallet** for Mystery Gift–owned inventory only (when gated pack paths exist).
- User-vaulted NFTs, automated buybacks, and commission execution remain disabled for public alpha.

## Target Model (EVM — not Solana)

Settlement is **Solidity smart contracts** on:

| Chain | Role |
| --- | --- |
| **Base (8453)** | Primary **ERC-721 pack escrow** — Beezie (and other) graded-card NFTs creators already hold |
| **Robinhood Chain (4663)** | Platform **token**, **USDG** payment rails, optional **stock-token (ERC-20) packs** |
| Solana | Deferred for pack settlement (CollectorCrypt/Phygitals may return later) |

### Base: NFT packs

1. Creator `safeTransferFrom` NFTs into `PackEscrow721` (`createPack`).
2. Contract stores pack state, remaining token IDs, price (USDC), fee bps.
3. Buyer **pays USDC and commits** entropy (`buy`).
4. After a short block delay, buyer **reveals** (`open`); contract selects a **uniform** remaining NFT and transfers it out (commit-reveal — no operator RNG key).
5. Creator claims USDC proceeds (minus fee). **NFT custody never depends on a service wallet.**

### Robinhood Chain: token + RWA packs

1. Deploy `$CLAWMACHINE` (ERC-20) for brand, fees, and governance.
2. Optional `PackEscrow20`: creators deposit stock tokens (NVDA, SPY, …); buyers pay USDG; open returns a random prize slice.
3. Disclose EV with Chainlink feeds; check sequencer uptime and `oraclePaused()` on corporate actions.
4. Account abstraction (Alchemy / ZeroDev) for gas sponsorship and batched agent txs.

### Cross-chain

Robinhood messaging is **Ethereum L1 ↔ RH L2**, not Base ↔ RH. Do **not** design v1 packs that require atomic Base NFT + RH stock prize. Ship two products; bridge only later if needed.

## Required Gates

- Testnet prototype (Base Sepolia + RH testnet 46630) with failure-path tests.
- External audit before mainnet **user** inventory deposits.
- Multisig / timelock for upgrade and pause authority.
- Monitoring: escrow balances, failed opens, stuck packs, refund/cancel windows.

## Buybacks

Unavailable unless **atomic** NFT-for-stablecoin settlement is implemented. Delayed “send NFT then wait for admin payout” is rejected for public product.

## References

- [Deploy on Robinhood Chain](https://docs.robinhood.com/chain/deploy-smart-contracts)
- [Stock tokens](https://docs.robinhood.com/chain/building-with-stock-tokens)
- [Oracles](https://docs.robinhood.com/chain/oracles-and-price-feeds)
- [Token contracts (USDG, WETH, stocks)](https://docs.robinhood.com/chain/contracts)
- Contract scaffolds: `contracts/` in this repo
