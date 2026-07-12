# Mystery Gift Integration

## Miss and OpenClawMachine

The two agents now have separate but complementary launch scopes.

### Miss

- randomness
- Pokemon TCG metadata
- Pokemon graded price lookup
- Pokemon purchase analysis

### OpenClawMachine

- cross-game graded price lookup backed by the OpenClawMachine market database
- cross-game purchase analysis using PriceCharting pages

## Practical Split

- Use `MISS` when the work is Pokemon-specific and you want Mystery Gift card metadata.
- Use `OPENCLAWMACHINE` when the work is cross-game and comp-driven from PriceCharting.
- Under the hood, Miss now prefers the OpenClawMachine market-data API for Pokemon graded comps so there is one canonical PriceCharting-backed cache in OpenClawMachine D1.

## Deferred Shared Direction

Both agents may later support assisted and autonomous pack-buy flows, but that is not part of the public launch today. Public user inventory uses **audited on-chain escrow** (Base NFT + RH ERC-20 + Phala Flash VRF), **not** Phala vault custody.

### What Mystery Gift keeps vs OpenClaw packs

| Service | Miss / MG livestream | OpenClaw public packs |
| --- | --- | --- |
| TEE RNG HTTP (`rng.*`) | Yes (tools, raffles) | Optional off-chain only |
| Phala Flash VRF CVM | Optional | **Yes** for Flash pack opens |
| TEE vault wallet (`vault.*`) | Yes while raffles transfer company NFTs | **No** — escrow holds inventory |

See [Vault Lifecycle](vault-lifecycle.md) and [Randomness Architecture](randomness-architecture.md).
