# How It Works

## Today (live)

1. The user (or agent) supplies a direct PriceCharting product page, query, or plain-language request.  
2. OpenClawMachine refreshes or reads the stored market snapshot.  
3. Graded comps and recent sales are returned; analysis can score an ask price.  
4. The user decides whether to buy **elsewhere** (Beezie, eBay, Collector Crypt, etc.).  

## Next (not public yet)

### Base — NFT packs

1. Creator approves ERC-721 slabs and calls `createPack` on `PackEscrow721`.  
2. Buyer pays USDC and **commits** entropy (`buy`).  
3. After a short delay, buyer **reveals** (`open`) and receives a uniform random remaining NFT.  
4. Creator claims USDC proceeds (minus protocol fee).  

No Phala vault holds public inventory. Physical redemption remains with the NFT issuer.

### Robinhood Chain — token and optional RWA packs

1. Platform token and USDG rails for brand and fees.  
2. Optional `PackEscrow20`: stock-token prizes, USDG payment, same commit-reveal open.  
3. EV disclosure can use Chainlink stock feeds (off-chain or future on-chain checks).  

## Explicitly deferred

- Solana pack settlement  
- Atomic Base↔Robinhood packs  
- Instant buybacks without atomic settlement  
- ACP pack offerings until contracts + indexer are ready  

See [Product Narrative](narrative.md) and [Escrow V2](escrow-v2.md).
