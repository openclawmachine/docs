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
| **Base (`eip155:8453`)** | **NFT packs** — Pokemon, One Piece, Beezie-class graded ERC-721 via `PackEscrow721Flash` (USDC) |
| **Robinhood Chain (`eip155:4663`)** | Platform token **$CLAWMACHINE**; **equity / stock-token packs** + **AI agent & meme token packs** (e.g. cashcat, hoodies, vexai) via `PackEscrow20Flash` (USDG) |
| **Solana** | **Deferred** for pack settlement (CollectorCrypt / Phygitals may return later) |

Physical cards stay with Beezie / Collector Crypt / graders. OpenClaw does **not** intake, insure, or ship physical inventory.

**Custody:** pack assets live in the **escrow smart contract**, not a Phala TEE vault wallet. See [Vault Lifecycle](vault-lifecycle.md).

## How we differ from Beezie / Collector Crypt

| | Beezie / Collector Crypt | OpenClaw target |
| --- | --- | --- |
| Physical vault | Core business | Out of scope |
| Who stocks gacha | Platform | **Creators** (permissionless escrow) |
| Settlement | Platform treasury | **Smart contracts** (Base / RH) |
| Live product today | Marketplace + gacha | **Analysis only** |
| Open source pack contracts | No | **Yes (MIT, not audited yet)** |

## Randomness (honest wording)

**Preferred (production packs):** [Phala Flash VRF](randomness-architecture.md) — on-chain request, TEE-signed fulfill, uniform pick over remaining reserved inventory. Trust root = Phala TEE + registered pubkey (not classical Chainlink ECVRF).

**Fallback:** buyer **commit-reveal** (`PackEscrow721` / `PackEscrow20` without Flash).

Do **not** say “Chainlink VRF on Robinhood” (VRF not available there). Do **not** say “provably fair against all adversaries” for Flash without naming TEE trust. Do say: **uniform over remaining; escrowed inventory; Flash TEE-signed or commit-reveal**.

## Custody (honest wording)

- **Public packs:** assets sit in the **escrow contract**, not a Phala hot wallet.  
- **TEE vault wallet is not required** for public pack create/open — see [Vault Lifecycle](vault-lifecycle.md).  
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

- [Randomness Architecture](randomness-architecture.md)  
- [Vault Lifecycle](vault-lifecycle.md)  
- [Flash VRF Ops](flash-vrf-ops.md)  
- [Escrow V2](escrow-v2.md)  
- [Chain Support](chain-support.md)  
- [Roadmap](roadmap.md)  
- [Economics](economics.md)  
- Contracts: `contracts/` in the OpenClaw Machine monorepo  
