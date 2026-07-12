# Vault Lifecycle: TEE Wallet vs Smart-Contract Escrow

**Question:** With permissionless packs on Solidity + Flash VRF, do we still need the Phala **TEE vault wallet** app (`vault.mysterygift.fun`)?

**Answer:** **Not for public packs.** Escrow contracts replace vault custody for OpenClaw pack inventory. Keep (or sunset deliberately) the vault only for **legacy / company-stock / Mystery Gift livestream** paths that still move assets from a hot wallet.

---

## Roles (do not conflate)

| Component | Holds user/creator assets? | Signs prize transfer? | Still needed for SC packs? |
| --- | --- | --- | --- |
| **`PackEscrow721Flash` / `PackEscrow20Flash`** | **Yes** (the contract) | Contract `safeTransfer*` on open | **Yes — this is the product** |
| **`PhalaFlashVRFCoordinator` + Flash CVM** | No | No (only randomness + ECDSA) | Yes for Flash opens |
| **TEE RNG HTTP** (`rng.*`) | No | No | Optional entropy for agents/raffles; not pack custody |
| **TEE vault wallet** (`vault.*`) | **Would** hold NFTs in a key-managed wallet | Yes (`/transfer-nft`) | **No for public packs** |
| **Legacy `gacha.ts` / pull path** | Via vault | Via vault | **Gated / company-stock only** — not public |

---

## Public product (OpenClaw packs)

```
Creator → approve + createPack → assets in ESCROW CONTRACT
Buyer  → buy → Flash VRF → settle → assets to BUYER wallet
Creator → claimProceeds → payment token to CREATOR
```

- **No** “deposit NFT into Phala vault”
- **No** `TEE_VAULT_API_KEY` in the open path
- **No** shared company wallet holding many creators’ inventory
- Randomness is **Flash coordinator** (or commit-reveal), not vault

So for **Base NFT packs** and **RH equity/meme packs**, the vault wallet app is **out of scope**.

---

## When the vault wallet still exists in the monorepo

Mystery Gift / OpenClaw still have code and CVMs for:

1. **Mystery Gift livestream raffles** — company-owned Solana NFTs transferred to winners via TEE vault  
2. **Legacy gated pack APIs** — `gacha.ts` / `pull.ts` paths that assume vault holds mints (must stay execution-gated; never marketed as public)  
3. **Internal ops** — if ops still move company inventory without deploying escrow

These are **orthogonal** to permissionless EVM packs. Shipping Flash packs does **not** automatically delete the vault CVM; it **removes the requirement** that public creators use it.

---

## Deprecation policy (recommended)

| Phase | Action |
| --- | --- |
| **Now** | Document: public packs = escrow only; vault = legacy/company |
| **When Base/RH packs are testnet-live** | Disable public vault deposit UX everywhere; keep vault for raffle agent if still Solana |
| **When raffles migrate or inventory is empty** | Plan CVM teardown: remove `vault.*` routes from api-proxy, stop vault CVM, archive docs |
| **Do not** | Delete vault code blindly while livestream still transfers via TEE |

### OpenClaw API

- Keep execution gates on vault-backed routes (`execution-gate` middleware).  
- Skill / docs / landing: **never** instruct agents to deposit into vault for packs.  
- Point pack creation docs at `createPack` on escrow addresses once deployed.

### Mystery Gift monorepo

- Livestream server may still set `TEE_VAULT_*` until raffle NFT source changes.  
- Marketplace “vault inventory” language for **public** gacha should be retired in favor of escrow narrative.

---

## What you still run on Phala

| CVM / service | Purpose after SC packs |
| --- | --- |
| **Flash VRF CVM** | Fulfill on-chain randomness for packs (**new**) |
| **RNG HTTP CVM** | Miss tools, raffles, x402 seeds (**keep**) |
| **Miss agent CVM** | Conversational agent (**keep**) |
| **Vault wallet CVM** | Only if raffles/company inventory still need signed transfers (**optional → deprecate**) |

**Net:** smart contracts replace the vault for **pack custody and settlement**. They do **not** replace every TEE service.

---

## Security comparison

| Risk | TEE vault model | Escrow + Flash model |
| --- | --- | --- |
| Commingled inventory | High (one wallet) | Low (per-contract, per-pack arrays) |
| Operator steals prize | Vault key / API abuse | Must break contract or pause governance |
| Biased open | Operator/API RNG | TEE key + on-chain verify (Flash) or commit-reveal |
| Stuck funds | Failed transfer after pull | Refund timeout + pause + claim patterns |
| Key management | Enclave wallet sk | Enclave **signing** sk for VRF only; assets in contract |

---

## FAQ

**Q: Can we turn off `vault.mysterygift.fun` tomorrow?**  
A: Only if nothing still depends on it (raffles, internal tools). For **OpenClaw public packs**, yes you can refuse new deposits now. For **Mystery Gift livestream**, check agent config first.

**Q: Does Flash VRF need the vault wallet?**  
A: No. Flash needs a **gas-funded TEE operational wallet** (different key, no NFT custody).

**Q: Do creators still “trust Phala”?**  
A: For Flash opens they trust the **TEE for randomness**. For **custody** they trust the **audited-or-reviewable Solidity escrow**, not a hot wallet.

**Q: Solana packs?**  
A: Deferred. Vault remains the historical Solana path; not the v1 public product.

---

## See also

- [Randomness Architecture](randomness-architecture.md)
- [Escrow V2](escrow-v2.md)
- [Product Narrative](narrative.md)
