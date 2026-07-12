# Chain Support

## Live (analysis / data)

Chain IDs matter less for PriceCharting-backed graded lookup, which is game/data-centric:

- Pokemon, One Piece, Yu-Gi-Oh, Magic, Lorcana — market database from PriceCharting

Payment for ACP analysis today: USDC on Solana/Base via facilitators; Robinhood **USDG** is the preferred EVM expansion rail.

## Settlement chains (packs / token)

| Chain | CAIP-2 | Role |
| --- | --- | --- |
| **Base** | `eip155:8453` | **NFT packs** (Pokemon, One Piece, Beezie-class) via `PackEscrow721Flash` + Flash VRF |
| **Robinhood Chain** | `eip155:4663` | `$CLAWMACHINE`, USDG, **equity + AI/meme ERC-20 packs** via `PackEscrow20Flash` |
| Robinhood Testnet | `eip155:46630` | Contract deploys / dry runs |
| Solana | — | **Deferred** for pack settlement |

### Robinhood Chain endpoints

| | Mainnet | Testnet |
| --- | --- | --- |
| Chain ID | 4663 | 46630 |
| RPC | `https://rpc.mainnet.chain.robinhood.com` | `https://rpc.testnet.chain.robinhood.com` |
| Explorer | [blockscout](https://robinhoodchain.blockscout.com) | [testnet explorer](https://explorer.testnet.chain.robinhood.com) |
| USDG | `0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168` | (confirm on testnet) |
| Permit2 | `0x000000000022D473030F116dDEE9F6B43aC78BA3` | same |

### Base

| | Mainnet |
| --- | --- |
| Chain ID | 8453 |
| USDC | `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` |

## What is deferred

- Solana program-owned pack escrow (CollectorCrypt / Phygitals inventory)
- Atomic multi-chain packs (Base NFT prize + RH stock prize in one open)
- User deposits into Phala TEE vaults for public packs
- Automated buybacks without atomic settlement

Phala remains useful for **Flash VRF** (on-chain pack opens) and **HTTP RNG** (agents/raffles). The **TEE vault wallet is not used for public pack custody** — see [Vault Lifecycle](vault-lifecycle.md) and [Randomness Architecture](randomness-architecture.md).
