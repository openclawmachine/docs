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

Both agents will later support assisted and autonomous pack-buy flows, but that is not part of the public launch today.
