# Escrow V2 (Base + Robinhood Chain)

OpenClawMachine alpha is analysis-first. Public users must **not** deposit NFTs into a Phala/company service wallet.

## Current Policy

- Live product: graded prices, recent sales, listing analysis, market-data catalog.
- Phala vault signing is a **company hot wallet** for Mystery Gift–owned inventory only (when gated pack paths exist).
- User-vaulted NFTs, automated buybacks, and commission execution remain disabled for public alpha.
- **Public packs do not need the TEE vault wallet** — escrow contracts hold assets. Details: [Vault Lifecycle](vault-lifecycle.md).

## Target Model (EVM — not Solana)

Settlement is **Solidity smart contracts** on:

| Chain | Role |
| --- | --- |
| **Base (8453)** | **ERC-721 NFT packs** — Pokemon, One Piece, Beezie-class graded cards (`PackEscrow721Flash`) |
| **Robinhood Chain (4663)** | Platform **token**, **USDG** rails, **equity + AI/meme ERC-20 packs** (`PackEscrow20Flash`) |
| Solana | Deferred for pack settlement (CollectorCrypt/Phygitals may return later) |

### Base: NFT packs (Flash preferred)

1. Creator `safeTransferFrom` NFTs into `PackEscrow721Flash` (`createPack`).
2. Buyer pays **USDC**, contract **reserves** a slot and requests **Phala Flash VRF**.
3. TEE fulfills on-chain; contract (push or `settle`) picks a **uniform** remaining NFT and transfers to buyer.
4. Creator `claimProceeds`. **No TEE vault custody.**

Fallback without Flash CVM: `PackEscrow721` commit-reveal (see contracts README).

### Robinhood Chain: equity + meme/AI packs

1. Deploy `$CLAWMACHINE` (ERC-20) for brand, fees, and governance.
2. `PackEscrow20Flash`: creators deposit **stock tokens** and/or **RH-chain AI/meme tokens**; buyers pay **USDG**; Flash open returns one prize.
3. Disclose EV (Chainlink price feeds on RH where available); check sequencer uptime and `oraclePaused()` for corporate actions on equities.
4. Account abstraction (Alchemy / ZeroDev) for gas sponsorship and batched agent txs.

Fallback: `PackEscrow20` commit-reveal.

### Randomness

See **[Randomness Architecture](randomness-architecture.md)** and **[Flash VRF Ops](flash-vrf-ops.md)**.  
Chainlink VRF is optional on Base only; **not available on Robinhood** as of this writing.

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
