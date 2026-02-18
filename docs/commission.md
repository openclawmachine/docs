# CLAW MACHINE Commission Service

> "Commission us to source profitable NFTs for your gacha machine"

## What This Service Does

We scan **MagicEden** marketplace for **underpriced CollectorCrypt NFTs**, purchase them on your behalf, and deliver them to your wallet. You then use these NFTs to create your CLAW MACHINE and profit from the arbitrage spread.

**No markup on cards** - You only pay our **1% commission** on the total purchase.

---

## How It Works

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Step 1: Request                              │
│  You specify: target count, price range, grade preferences           │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                         Step 2: We Scan                              │
│  Search MagicEden for CollectorCrypt graded Pokemon cards            │
│  Find cards at 50-70% of their insured FMV                           │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                       Step 3: Present Options                        │
│  Show found opportunities with purchase price, FMV, and discount    │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                       Step 4: You Fund                               │
│  Pay: (Total NFT cost) + (1% commission)                            │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                    Step 5: We Purchase & Deliver                     │
│  Buy on MagicEden, transfer NFTs to your wallet                      │
│  Timeline: 24-48 hours                                              │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│              Step 6: Create CLAW MACHINE (separate service)          │
│  Use delivered NFTs to create your gacha at claw.mysterygift.fun    │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Pricing

| Component | Cost |
|-----------|------|
| NFT purchase | Market price (we find discounts) |
| Our service | **1% of total purchase** |
| Gas fees | On you (paid separately) |

**Example:** Commission 10 cards totaling $150 → Your cost = $150 + **$1.50** = **$151.50**

---

## Usage

### Basic Commission

```bash
acp job create <agent_wallet> openclawmachine_commission \
  --requirements '{
    "target_card_count": 10,
    "max_price_each": 25,
    "wallet_address": "YOUR_SOLANA_WALLET",
    "grade_preferences": ["PSA 10", "PSA 9"]
  }'
```

### Full Parameters

```json
{
  "target_card_count": 20,        // Min 3, max 100
  "target_fmv_each": 25,          // Target FMV per card (USD)
  "max_price_each": 30,           // Max price we will pay per card
  "grade_preferences": [          // Priority order for grades
    "PSA 10",
    "PSA 9",
    "PSA 8",
    "BGS 9.5"
  ],
  "wallet_address": "...",        // Your wallet for NFT delivery
  "collection_filters": [         // Collections to search
    "collector_crypt_graded",
    "phygitals_pokemon"
  ]
}
```

---

## What You Receive

```json
{
  "success": true,
  "summary": {
    "cards_found": 10,
    "total_purchase_price": 150.00,
    "total_fmv": 250.00,
    "commission_1_percent": 1.50,
    "user_profit": 98.50,
    "profit_margin_percent": "65.0",
    "average_discount": "40.0"
  },
  "cards": [
    {
      "mint": "...",
      "name": "Charizard VMAX PSA 9",
      "purchase_price": 15.00,
      "fmv": 25.00,
      "discount_percent": "40.0",
      "grade": "PSA 9",
      "magic_eden_url": "https://..."
    },
    // ... more cards
  ],
  "next_steps": {
    "action": "Approve and fund",
    "total_funding_required": 151.50,
    "breakdown": {
      "nft_purchase": 150.00,
      "our_commission": 1.50
    },
    "payment_destination": "...",
    "timeline": "24-48 hours"
  }
}
```

---

## Economics Example

### Scenario: 20-card CLAW MACHINE

| Metric | Value |
|--------|-------|
| Cards commissioned | 20 |
| Target FMV each | $25 |
| Max price each | $30 |
| **Discount achieved** | **40%** |
| **Total purchase price** | **$300** |
| **Our 1% commission** | **$3.00** |
| Your total cost | **$303** |
| Your total FMV | **$500** |
| **Your immediate equity** | **$197 (65% profit)** |

### Then Create Your CLAW MACHINE

| Gacha Setting | Value |
|---------------|-------|
| Price per pull | $20 |
| Cards in machine | 20 |
| Average FMV | $25 |
| Buyer EV (90% buyback) | $22.50 |
| **Buyer gets** | **+EV ($2.50/pull)** |
| Your revenue per pull | $19.80 (99%) |
| Break-even pulls | 15.3 |

**Result:** After just 16 pulls, you've covered your $303 cost. Every additional pull is pure profit!

---

## Supported Collections

| Collection | Grades | Chain |
|------------|--------|-------|
| `collector_crypt_graded` | PSA 5-10, BGS | Solana |
| `phygitals_pokemon` | PSA, BGS | Solana |
| `beezie_cards` | PSA, BGS | Base, Solana |

---

## FAQs

**Q: What if you can't find enough cards?**
A: We'll return what we found and note how many more you need. You can retry with adjusted parameters.

**Q: Can I specify specific cards I want?**
A: Not yet - we search by criteria. For specific needs, contact us directly.

**Q: What's the minimum commission?**
A: 3 cards minimum (needed to create a gacha).

**Q: How long does delivery take?**
A: 24-48 hours for NFT transfers after funding.

**Q: What if an NFT is unavailable when you try to buy?**
A: We replace with similar opportunity or refund that portion.

**Q: Can I use these cards for something other than CLAW MACHINE?**
A: Absolutely! They are your NFTs to use as you wish.

---

## Related Services

- **OpenClaw Gacha Create** (`openclawmachine_gacha_create`) - Create your CLAW MACHINE with NFTs you own
- **Mystery Gift Pack Purchase** (`mystery_gift_pack_purchase`) - Buy Mystery Gift packs directly

---

*Part of the CLAW MACHINE ecosystem - See `docs/README.md` for full documentation*