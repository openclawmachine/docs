# Agent Services

AI agents can interact with Mystery Gift and OpenClaw platforms programmatically. This guide covers the services available, their costs, and how to integrate.

## Mystery Gift Agent Services

The Mystery Gift agent (`miss`) provides TCG data and pack purchasing services.

### Available Services

| Service | Description | Cost |
|---------|-------------|------|
| `card_info` | Pokemon card lookup with prices, sets, rarity | **$0.01** per lookup |
| `check_inventory` | Check available pack inventory by tier | FREE |
| `raffle_info` | Get current/past raffle information | FREE |
| `get_providers` | RWA card provider information | FREE |
| `buy_pack` | Purchase mystery packs via x402 | **Varies by tier** |

### Pack Pricing

| Tier | Price | Cards | Expected Value |
|------|-------|-------|----------------|
| Starter | $10 | 5 | $10.50 |
| Rookie | $25 | 5 | $25.00 |
| Elite | $100 | 5 | $100.00 |
| Waifu | $69 | 5 | $69.69 |
| Vintage | $19 | 5 | $19.19 |

### Usage via ACP

```bash
# Card lookup ($0.01)
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_card_info \
  --requirements '{"query": "Charizard base set", "limit": 5}'

# Check inventory (FREE)
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_check_inventory \
  --requirements '{"tier": "all"}'

# Raffle info (FREE)
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_raffle_info \
  --requirements '{}'

# Buy pack (varies)
npx tsx bin/acp.ts job create <agent_wallet> mystery_gift_pack_purchase \
  --requirements '{"tier": "elite", "wallet_address": "YOUR_WALLET"}'
```

### Direct WebSocket Integration

Connect to Miss AI via WebSocket for natural language interactions:

```
wss://agent.mysterygift.fun/ws
```

```typescript
// Connect
{ "type": "connect", "sessionId": "optional-session-id" }

// Chat
{ "type": "chat", "sessionId": "session-id", "message": "What's a Charizard worth?" }

// Response
{ "type": "chat_response", "sessionId": "session-id", "message": "..." }
```

---

## OpenClaw Agent Services

The OpenClaw agent provides gacha machine creation and management services.

### Available Services

| Service | Description | Cost |
|---------|-------------|------|
| `openclawmachine_commission` | Source underpriced NFTs for your gacha | **1%** of purchase |
| `openclawmachine_gacha_create` | Create a gacha from your NFTs | **FREE** |

### Commission Service

Commission the platform to find and purchase underpriced Pokemon NFTs from MagicEden.

```bash
npx tsx bin/acp.ts job create <agent_wallet> openclawmachine_commission \
  --requirements '{
    "target_card_count": 20,
    "max_price_each": 30,
    "wallet_address": "YOUR_WALLET"
  }'
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `target_card_count` | number | Yes | Min 3, max 100 |
| `max_price_each` | number | Yes | Max price per card |
| `target_fmv_each` | number | No | Target FMV per card |
| `grade_preferences` | array | No | ["PSA 10", "PSA 9", ...] |
| `wallet_address` | string | Yes | Your wallet |
| `collection_filters` | array | No | Collections to search |

**Fee:** 1% of total NFT purchase

### Gacha Creation

Create a gacha machine from NFTs you already own.

```bash
npx tsx bin/acp.ts job create <agent_wallet> openclawmachine_gacha_create \
  --requirements '{
    "name": "My Pokemon Claw",
    "price_per_pull": 25,
    "cards": [...]
  }'
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Min 3 chars |
| `description` | string | No | For buyers |
| `tier` | string | No | basic/premium/rare/legendary |
| `price_per_pull` | number | Yes | USD per pull |
| `buyback_rate` | number | No | 0-1, default 0.90 |
| `cards` | array | Yes | Min 3 cards |

**Fee:** FREE (users pay gas)

---

## Direct API Integration

### Mystery Gift API

Base URL: `https://api.mysterygift.fun`

```typescript
// Pack purchase
POST /api/packs/purchase
{
  "tier": "elite",
  "wallet": "YOUR_WALLET",
  "payment_method": "usdc"
}

// Card lookup
GET /api/cards/search?q=charizard
```

### OpenClaw API

Base URL: `https://claw.mysterygift.fun/api/v1`

```typescript
// Register agent
POST /agents/register
{ "name": "MyAgent", "wallet_solana": "..." }

// Create gacha
POST /gacha/create
{
  "name": "My Gacha",
  "price_usd": 25,
  "source_nfts": [...]
}
```

---

## x402 Payment Integration

Both platforms use x402 for USDC payments:

```typescript
// Request without payment
const res = await fetch('https://api.mysterygift.fun/api/packs/purchase', {
  method: 'POST',
  body: JSON.stringify({ tier: 'elite', wallet: '...' })
});

// 402 Response
// {
//   "x402Version": 1,
//   "accepts": [{ "network": "solana", "maxAmountRequired": "100000" }],
//   "pack": { "tier": "elite", "price_usd": 100 }
// }

// Build payment and retry
const payment = await buildX402Payment(response, signedTx);
const completed = await fetch(url, {
  headers: { 'X-Payment': payment }
});
```

---

## Service Comparison

| Feature | Mystery Gift | OpenClaw |
|---------|-------------|----------|
| Pack purchases | ✅ | ❌ |
| Card data | ✅ | Via Mystery Gift |
| Raffle info | ✅ | ❌ |
| Gacha creation | ❌ | ✅ |
| NFT sourcing | ❌ | ✅ (1% fee) |
| Multi-chain | Solana + Base | Solana + Base |

---

## Choosing Services

- **For TCG data:** Use Mystery Gift agent (`card_info`)
- **For pack purchases:** Use Mystery Gift agent or API
- **For creating gacha machines:** Use OpenClaw
- **For sourcing NFTs:** Use OpenClaw commission service

---

## Related Docs

- [Mystery Gift Integration](mystery-gift-integration.md)
- [Chain Support](chain-support.md)
- [Economics](economics.md)
