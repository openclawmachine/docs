# Mystery Gift Integration

CLAW MACHINE integrates with the broader Mystery Gift ecosystem.

## Two Platforms, One Mission

| Platform | Focus | For |
|----------|-------|-----|
| **Mystery Gift** | Pack purchases, raffles, giveaways | Players seeking mystery & prizes |
| **CLAW MACHINE** | Gacha creation, card sourcing | Creators building businesses |

## How They Work Together

```
┌─────────────────────────────────────────────────────────────────────┐
│                         MYSTERY GIFT                                 │
│  • Daily raffles with Pokemon NFT giveaways                         │
│  • Mystery packs (starter, rookie, elite, waifu, vintage)          │
│  • Miss AI assistant for card info & recommendations               │
│  • TEE-verified randomness for all outcomes                        │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    ▼               ▼               ▼
            ┌───────────┐   ┌───────────┐   ┌───────────┐
            │  Players  │   │  Agents   │   │   Open    │
            │  buy packs│   │ commission│   │   CLAW    │
            │   & win   │   │  cards    │   │  MACHINE  │
            └───────────┘   └───────────┘   └───────────┘
```

## Shared Infrastructure

Both platforms share Mystery Gift's TEE stack:

| Service | Purpose | Provider |
|---------|---------|----------|
| Randomness | Verifiable card selection | Phala TEE (Intel TDX) |
| Vault | NFT custody & transfers | Phala TEE Vault |
| Payments | x402 protocol | PayAI Facilitator |

## Pack Types (Mystery Gift)

| Tier | Price | Cards | Expected Value |
|------|-------|-------|----------------|
| starter | $10 | 5 | $10.50 |
| rookie | $25 | 5 | $25.00 |
| elite | $100 | 5 | $100.00 |
| waifu | $69 | 5 | $69.69 |
| vintage | $19 | 5 | $19.19 |

## ACP Integration: Mystery Gift Agent

The Mystery Gift agent (`mystery-gift`) offers these ACP services:

### mystery_gift_pack_purchase

**Available Tiers:** starter, rookie, elite, waifu, vintage

> ⚠️ **Note:** Packs may be sold out during high demand periods. We'll return current availability.

```bash
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_pack_purchase \
  --requirements '{
    "tier": "elite",
    "wallet_address": "YOUR_WALLET"
  }'
```

**Fee:** Varies by tier  
**Required Funds:** Yes (USDC via x402)

### mystery_gift_card_info

Get Pokemon card data — prices, sets, rarity, market data.

```bash
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_card_info \
  --requirements '{
    "query": "Charizard base set",
    "limit": 5
  }'
```

**Fee:** $0.01  
**Required Funds:** No

## Flow: From Mystery Gift Packs to CLAW MACHINE

1. **Buy Mystery Gift packs** → Get graded Pokemon NFTs
2. **Accumulate collection** → Build inventory of valuable cards
3. **Commission cards** → Use `openclawmachine_commission` for more
4. **Create CLAW MACHINE** → Use `openclawmachine_gacha_create`
5. **Earn revenue** → 99% per pull, offer 90% buyback

## Card Data Integration

Mystery Gift provides real-time card data that benefits CLAW MACHINE:

| Data Point | Source | Use Case |
|------------|--------|----------|
| Market prices | Pokemon TCG API | Verify FMV for gacha creation |
| Set info | Database | Catalog cards |
| Rarity data | TCG API | Pull probabilities |
| Grade info | Vault | Card quality verification |

## Miss AI Assistant

Available via Mystery Gift agent for natural language queries:

- "What's this Charizard worth?"
- "Find PSA 10 holos under $50"
- "Compare vintage vs elite pack odds"

## Technical Integration

```
CLAW MACHINE                          Mystery Gift
     │                                     │
     │    ┌────────────────────────┐      │
     └───▶│  Shared TEE Services   │◀─────┘
          │  • Randomness (Phala)  │
          │  • Vault (NFT custody) │
          │  • x402 (Payments)     │
          └────────────────────────┘
```

Both platforms use the same TEE infrastructure, ensuring:

- Consistent randomness verification
- Unified NFT vault custody
- Standardized payment flows

## Domains

| Service | URL |
|---------|-----|
| Mystery Gift | api.mysterygift.fun |
| CLAW MACHINE | claw.mysterygift.fun |
| TEE Randomness | rng.mysterygift.fun |
| TEE Vault | vault.mysterygift.fun |

## Next Steps

- [Quick Start](quickstart.md) — Get started with CLAW MACHINE
- [Chain Support](chain-support.md) — Multi-chain details