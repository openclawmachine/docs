# FAQ

Frequently asked questions about CLAW MACHINE.

## General

### What is CLAW MACHINE?

CLAW MACHINE is an NFT gacha platform where creators deposit graded Pokemon cards, buyers pay to pull cards with TEE-verified randomness, and creators earn revenue.

### How is it different from other gacha platforms?

1. **TEE Verifiable Randomness** — Intel TDX hardware-backed, no manipulation possible
2. **Solvency Enforcement** — Platform ensures creators can cover buybacks
3. **Agent Commerce Protocol** — AI agents can programmatically create gachas
4. **ACP Commission Service** — We find underpriced NFTs for your gacha

### What NFTs are supported?

Graded Pokemon cards from:
- **CollectorCrypt** (primary)
- **Phygitals**
- **Beezie**

## Creating Gachas

### How much does it cost to create a gacha?

**FREE.** No platform fee for creation. You only pay gas fees for NFT transfers.

### What are the requirements?

- Minimum 3 cards
- NFTs must be in the TEE vault
- Must pass solvency check: `price × cards × 0.99 ≥ sum(values) × buyback_rate`
- 24-hour cooldown before going live

### Can I modify a gacha after creation?

No. Once created, the card pool is locked. This prevents manipulation.

### What's the 24-hour cooldown for?

Prevents front-running and gives buyers time to research the gacha before purchases begin.

## Buying & Pulling

### How much does a pull cost?

Set by the gacha creator. Typical range: $10-$50.

### What is the buyback rate?

Set by the creator, default is 90%. This is what sellers receive if they return the card.

### How is randomness verified?

Every pull uses Intel TDX hardware-backed randomness from Phala Network. The seed is verifiable — you can confirm it was generated in a secure enclave.

### What happens if my NFT transfer fails?

The platform will retry automatically. If retries fail, contact support with the opening ID.

## ACP & AI Agents

### What is ACP?

The Agent Commerce Protocol allows AI agents to programmatically interact with CLAW MACHINE. Agents can:
- Commission card sourcing
- Create gacha machines
- Manage inventory

### How do AI agents use this?

```bash
# Commission 20 cards
npx tsx bin/acp.ts job create <agent> openclawmachine_commission \
  --requirements '{"target_card_count": 20, "max_price_each": 30}'

# Create gacha
npx tsx bin/acp.ts job create <agent> openclawmachine_gacha_create \
  --requirements '{"name": "My Claw", "price_per_pull": 25, "cards": [...]}'
```

## Commission Service

### What is the commission service?

We scan MagicEden for underpriced CollectorCrypt NFTs, purchase them, and deliver to your wallet. You only pay our 1% commission.

### How much does the commission cost?

1% of total NFT purchase amount. Example: $300 in cards = $3 commission.

### How long does delivery take?

24-48 hours for NFT transfers.

### Can I specify which cards I want?

Not yet. We search by criteria (grade, price range, collection). For specific needs, contact us directly.

## Economics

### How much can I earn?

Depends on your sourcing and pricing. See [Economics](economics.md) for detailed breakdowns.

### What's the platform fee?

1% per pull. That's it.

### Do I pay for buybacks?

Yes, but only when buyers choose to sell back. The solvency check at creation ensures you have sufficient funds to cover expected buybacks.

### What's a good profit margin?

If you source at 40-50% below FMV and price pulls at 75-80% of FMV, you can achieve 50-100% margins.

## Troubleshooting

### My gacha creation was rejected

Most likely the solvency check failed. Your cards' total FMV × buyback_rate is too high relative to your pull price.

### NFT transfer failed

Try the retry endpoint or contact support with your opening ID.

### Payment not processing

Ensure you're using the correct network (Solana mainnet) and have sufficient USDC balance.

## Support

- **Discord**: [discord.gg/mysterygift](https://discord.gg/mysterygift)
- **Twitter**: [@mysterygift](https://twitter.com/mysterygift)
- **GitHub**: [github.com/anomalyco/mystery-gift](https://github.com/anomalyco/mystery-gift)