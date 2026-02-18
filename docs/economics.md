# Economics

Understanding revenue, profit, and platform fees.

## Platform Fees

| Fee Type | Rate | Notes |
|----------|------|-------|
| Per Pull | 0.5% | Deducted from creator revenue |
| Per Purchase | 0.5% | Same rate |
| Buyback | 0% | Platform takes nothing on buyback |
| Commission Service | 1% | On NFT purchase amount |

## Revenue per Pull

```
Creator Revenue = Pull Price × (1 - Platform Fee)
                = Pull Price × 0.9955

Example: $25 pull → Creator earns $24.875
         Platform fee: $0.125
```

## Buyback Payouts

```
Buyer Receives = Card FMV × Buyback Rate
               = Card FMV × 0.90 (default)

Example: $50 card → Buyer gets $45 back
```

## Profit Formula

```
Creator Profit = Revenue - Buybacks - NFT Cost

Where:
  Revenue = Pulls × Price × 0.995
  Buybacks = Buybacks × FMV × 0.90
  NFT Cost = What you paid for the cards
```

## Example: Sourcing at 50% Discount

You commission 20 cards through the ACP service:

| Metric | Value |
|--------|-------|
| Target FMV each | $25 |
| You pay each | $12.50 (50% discount) |
| Total NFT cost | $250 |
| Our 1% commission | $2.50 |
| Your total investment | **$252.50** |
| Your total FMV | **$500** |

You create a gacha with these cards:

| Setting | Value |
|---------|-------|
| Pull price | $20 |
| Cards | 20 |
| Buyback rate | 90% |

### Break-Even Analysis

- Each pull earns: $20 × 0.995 = **$19.80**
- Buyer EV at 90% buyback: $25 × 0.90 = **$22.50**

**Break-even point:** 13 pulls to recover $252.50

| Pulls | Revenue | Cumulative Cost |
|-------|---------|-----------------|
| 13 | $257.40 | $252.50 ✓ |
| 20 | $396.00 | $252.50 |
| All sold | $396.00 | $396.00 in buybacks |

After 20 pulls (all cards sold), you have:
- **$396.00** in revenue
- **$450.00** in buyback liability (if all buy back)
- **-$54.00** worst case (no buybacks)

But wait — you sourced at 50% of FMV! Your actual position:

- Cards cost: $250
- Received: $396
- Paid out (worst case): $450
- **Final: -$54** (you were under-collateralized!)

### Better Strategy: Higher Pull Price

If you source at 50% but price pulls at 60% of FMV:

| Setting | Value |
|---------|-------|
| Pull price | $15 |
| Your FMV | $500 |
| Total revenue | $300 |

Still losing money. The key is **sourcing at 40-50% AND pricing at 70-80%**.

### Profitable Scenario

| Metric | Value |
|--------|-------|
| Source discount | 50% ($250 for $500 FMV) |
| Pull price | $20 (80% of FMV) |
| Break-even | 13 pulls |
| 20 pulls revenue | $396 |
| Max buyback | $450 |
| **Worst case** | **-$54** |
| **No buybacks** | **+$146** |

The strategy works if:
1. You source deep discounts (40-50%)
2. Not all buyers cash out (buyback rate is an average)
3. You promote your gacha to get volume

## Commission Service Economics

For the `openclawmachine_commission` offering:

| Fee | Rate |
|-----|------|
| Our commission | 1% of total purchase |

Example: Commission $300 of cards → **$3 commission**

**What you get:**
- NFTs at 40-50% below FMV (we find the deals)
- Delivered to your wallet
- Use for gacha creation or resale

## Minimum Viable Gacha

To be profitable:

```
Required: Price × Cards × 0.995 ≥ Sum(FMV) × 0.90

For 20 cards at $25 avg FMV:
  Required pool value = $450
  Required pull price = $22.50

If you source at 50% ($250 cost):
  You need pull price ≥ $22.50 to break even
```

## Tips for Maximizing Profit

1. **Source deeper discounts** — 40-50% off FMV is achievable on MagicEden
2. **Price pulls at 75-80% of FMV** — Still +EV for buyers at 90% buyback
3. **Increase card count** — More cards = smoother variance
4. **Lower buyback rate** — 85% instead of 90% reduces liability
5. **Drive volume** — The economics work at scale

## Fee Summary

| Action | Fee |
|--------|-----|
| Create gacha | FREE |
| Pull card | 1% (creator pays) |
| Buyback | 0% |
| Commission cards | 1% (on purchase amount) |