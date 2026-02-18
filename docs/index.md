# CLAW MACHINE

> Build profitable NFT gacha machines with underpriced Pokemon cards.

CLAW MACHINE is an agent-first platform for creating and operating NFT gacha machines. Powered by Mystery Gift's TEE infrastructure (Intel TDX hardware-backed randomness), every pull is verifiably fair.

## What is CLAW MACHINE?

Think of it as a **Pokémon card vending machine** for the NFT era:

1. **Create**: Deposit graded Pokemon NFTs (PSA/BGS) into a gacha machine
2. **Buyers Pull**: Players pay to pull cards with TEE-verified randomness
3. **Earn Revenue**: You earn 99% of each pull (1% platform fee)
4. **Buyback**: Offer 90% buyback to keep players coming back

## Why Agents Choose CLAW MACHINE

| Feature | Benefit |
|---------|---------|
| TEE Verifiable Randomness | Intel TDX hardware-backed — no manipulation possible |
| Automated Solvency Checks | Platform enforces financial safety at creation |
| NFT Vault Custody | All NFTs held securely in TEE-protected wallet |
| x402 Payments | Seamless USDC payments via PayAI facilitator |
| ACP Integration | AI agents can commission cards and create gachas programmatically |

## Supported NFT Providers

- **CollectorCrypt** — Solana-native graded Pokemon cards
- **Phygitals** — Graded cards with physical redemption
- **Beezie** — Cross-chain cards with vault storage

## Quick Links

- [Quick Start](quickstart.md) — Get started in 5 minutes
- [ACP Integration](acp-overview.md) — For AI agents
- [Mystery Gift Integration](mystery-gift-integration.md) — Buy packs and commission cards
- [FAQ](faq.md) — Common questions

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        CLAW MACHINE Stack                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐  │
│  │  AI Agent (ACP) │───▶│  Cloudflare     │───▶│  Cloudflare D1  │  │
│  │                 │    │  Workers API    │    │  Database       │  │
│  └─────────────────┘    └─────────────────┘    └─────────────────┘  │
│           │                      │                     ▲             │
│           │                      │                     │             │
│           ▼                      ▼                     │             │
│  ┌─────────────────┐    ┌─────────────────┐             │             │
│  │  Phala TEE      │    │   MagicEden     │             │             │
│  │  Randomness     │    │   Marketplace   │─────────────┘             │
│  │  (Intel TDX)    │    │                 │                           │
│  └─────────────────┘    └─────────────────┘                           │
│           │                      │                                    │
│           │                      ▼                                    │
│  ┌─────────────────┐    ┌─────────────────┐                           │
│  │  TEE Vault      │    │   CollectorCrypt│                           │
│  │  (NFT Custody)  │    │   NFTs          │                           │
│  └─────────────────┘    └─────────────────┘                           │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## Stats

| Metric | Value |
|--------|-------|
| Platform Fee | 1% |
| Default Buyback | 90% |
| Minimum Cards | 3 |
| Randomness | TEE-verified (Intel TDX) |
| Payments | USDC via x402 |

---

**Built with ❤️ by the Mystery Gift Team**

*Questions? [Join our Discord](https://discord.gg/mysterygift) or [follow us on Twitter](https://twitter.com/mysterygift)*