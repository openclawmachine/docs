# Solvency & Safety

Platform guarantees and safety mechanisms.

## Solvency Enforcement

Every gacha creation undergoes a solvency check:

```
REQUIRED: price × cards × 0.99 ≥ sum(card_fmv) × buyback_rate

If FALSE: Gacha creation REJECTED
```

### Example: Solvent Gacha

| Cards | Pull Price | Buyback | Card FMV Total | Check |
|-------|------------|---------|----------------|-------|
| 20 | $25 | 90% | $556 | (25×20×0.99) vs (556×0.90) = 495 vs 500 ✗ FAIL |

### Example: Insolvent Gacha

| Cards | Pull Price | Buyback | Card FMV Total | Check |
|-------|------------|---------|----------------|-------|
| 20 | $20 | 90% | $500 | (20×20×0.99) vs (500×0.90) = 396 vs 450 ✗ FAIL |

**This gacha would be rejected.** You can't cover buybacks.

## What the Platform Guarantees

| Guarantee | How It's Enforced |
|-----------|-------------------|
| NFTs exist in vault | On-chain verification at creation |
| Solvency | Formula enforced at creation |
| Randomness is fair | TEE hardware-backed (Intel TDX) |
| Transfers occur | Optimistic locking + on-chain verification |
| Buyback processing | Admin-batched with on-chain verification |

## What Is NOT Guaranteed

| Gap | Note |
|-----|------|
| Card value accuracy | Creator self-reports at creation |
| Market value | NFT prices can fluctuate |
| Buyback timing | Manual batching (24-48 hour delay) |
| SOL/USD conversion | Direct comparison, no oracle |

## TEE Randomness Verification

Every pull uses hardware-verifiable randomness:

1. **Seed Generation**: Intel TDX enclave generates random seed
2. **Attestation**: Cryptographic proof from hardware
3. **Verification**: Platform verifies attestation before using seed
4. **Selection**: `card_index = seed % pool_size`

**You cannot:**
- Predict the next card
- Manipulate the outcome
- Front-run the system

## NFT Vault Security

| Aspect | Security Measure |
|--------|------------------|
| Private key | Never exposed — lives in TEE enclave |
| Transfers | Only via TEE-signed transactions |
| Authorization | `TEE_VAULT_API_KEY` bearer token |
| Audit trail | All transfers logged with tx signatures |

## Buyer Protections

1. **Escrow** — Payment held until NFT transfer confirmed
2. **On-chain verification** — Every transfer verified via RPC
3. **Retry mechanism** — Failed transfers can be retried
4. **Buyback guarantee** — If creator has funds (solvency check passed)

## Creator Protections

1. **Platform fee only 1%** — Low cost of operation
2. **No upfront gacha fee** — Free to create
3. **Variance warnings** — System alerts if max/min ratio > 10x
4. **Card pool locked** — Once created, pool can't be modified

## Known Limitations

| Limitation | Impact | Mitigation |
|------------|--------|------------|
| Self-reported values | Creator could overstate | Due diligence required |
| No price oracle | SOL/USD may drift | Verify prices independently |
| Manual buyback payouts | 24-48hr delay | Platform monitors queue |
| Single vault wallet | NFTs commingled | TEE enforces authorized transfers only |

## Best Practices

### For Buyers
1. Verify card values on secondary markets before pulling
2. Check the gacha's solvency (ask the creator)
3. Consider buyback rate — higher is safer

### For Creators
1. Source cards at 40-50% below FMV
2. Price pulls at 75-80% of FMV
3. Keep buyback rate reasonable (85-90%)
4. Increase card count to reduce variance

## Emergency Procedures

| Scenario | Action |
|----------|--------|
| NFT transfer fails | Retry via `/pull/:openingId/retry-transfer` |
| Vault health issues | Platform pauses new purchases |
| Creator dispute | Contact support with tx hash |

## Reporting Issues

- **Discord**: [discord.gg/mysterygift](https://discord.gg/mysterygift)
- **GitHub Issues**: [github.com/anomalyco/mystery-gift/issues](https://github.com/anomalyco/mystery-gift/issues)