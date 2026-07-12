# Product Narrative (source of truth)

Use this page when writing marketing, agent skills, or partner copy. If another doc conflicts with this one, **this page wins** until intentionally updated.

## Live today

OpenClaw Machine is **analysis-first**:

- Cross-game **graded price lookup** and **purchase analysis**
- Data from a PriceCharting-backed market database (D1)
- ACP offerings: `openclawmachine_graded_price`, `openclawmachine_graded_analysis`
- Games: Pokemon, One Piece, Yu-Gi-Oh, Magic, Lorcana (and similar PriceCharting layouts)

## Not public yet

- Pack buying / claw-machine play for end users
- Permissionless pack creation on mainnet
- Autonomous buyer fulfillment / commissions
- Instant buybacks
- User deposits into any Phala/company vault

## What we are building next

**Open pack layer on open contracts** — not a physical vault business.

| Chain | Product |
| --- | --- |
| **Base (`eip155:8453`)** | `PackEscrow721` — creators escrow **ERC-721** slab NFTs they already hold (e.g. Beezie-class); buyers pay **USDC** and open packs |
| **Robinhood Chain (`eip155:4663`)** | Platform token **$CLAWMACHINE**, **USDG** payment rails, optional **stock-token packs** (`PackEscrow20`) |
| **Solana** | **Deferred** for pack settlement (CollectorCrypt / Phygitals may return later) |

Physical cards stay with Beezie / Collector Crypt / graders. OpenClaw does **not** intake, insure, or ship physical inventory.

## How we differ from Beezie / Collector Crypt

| | Beezie / Collector Crypt | OpenClaw target |
| --- | --- | --- |
| Physical vault | Core business | Out of scope |
| Who stocks gacha | Platform | **Creators** (permissionless escrow) |
| Settlement | Platform treasury | **Smart contracts** (Base / RH) |
| Live product today | Marketplace + gacha | **Analysis only** |
| Open source pack contracts | No | **Yes (MIT, not audited yet)** |

## Randomness (honest wording)

Pack contracts use **commit-reveal**:

1. Buyer **pays and commits** a hash of secret entropy  
2. After a short block delay, buyer **reveals** and receives a **uniform** random remaining prize  

There is **no privileged `rngSigner`** in the current design. Do **not** say “Chainlink VRF” or “provably fair against all adversaries” unless that system is actually integrated. Do say: **uniform over remaining inventory; buyer-bound commit-reveal; not operator-picked**.

## Custody (honest wording)

- **Public packs:** assets sit in the **escrow contract**, not a Phala hot wallet.  
- **Legacy code** under `gacha.ts` / TEE vault is **company-stock / gated** and is **not** the public product path.  
- **Never** market “deposit NFTs into our vault” for public creators.

## Token

`$CLAWMACHINE` on Robinhood Chain is a **platform token** (brand / fees / governance).  
It is **not** a claim on pack inventory and **not** a promise of pack revenue until on-chain fee routing is live and documented. Prefer multisig treasury before mainnet mint.

## Forbidden claims until true

- Packs / claw machine “live in production”  
- “Provably fair” without specifying commit-reveal limits  
- “Trustless operator cannot affect anything” if a privileged RNG is reintroduced  
- Instant buyback  
- Solana pack escrow as current plan  
- OpenClaw as a physical card vault  

## See also

- [Escrow V2](escrow-v2.md)  
- [Chain Support](chain-support.md)  
- [Roadmap](roadmap.md)  
- [Economics](economics.md)  
- Contracts: `contracts/` in the OpenClaw Machine monorepo  
