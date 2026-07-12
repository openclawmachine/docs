# Flash VRF Operations Runbook

Operational guide for running Phala Flash VRF against OpenClaw pack escrows.

## Architecture (one chain)

```
PackEscrow*Flash  ──request──►  PhalaFlashVRFCoordinator  ◄──onRandomGenerated──  Flash CVM (TEE)
        ▲                              │
        └──── rawFulfillRandomness ────┘  (push)
        └──── settle() pulls getRandom()     (pull)
```

Deploy **per chain** (Base and Robinhood are independent).

## Addresses (fill after deploy)

| Network | Chain ID | Coordinator | Escrow721Flash | Escrow20Flash | Payment |
| --- | --- | --- | --- | --- | --- |
| Base Sepolia | 84532 | _TBD_ | _TBD_ | — | test USDC |
| Base mainnet | 8453 | _TBD_ | _TBD_ | — | `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` |
| RH testnet | 46630 | _TBD_ | — | _TBD_ | test USDG / mock |
| RH mainnet | 4663 | _TBD_ | — | _TBD_ | `0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168` |

## Deploy contracts

```bash
cd contracts
export PRIVATE_KEY=0x...
export FEE_RECIPIENT=0xYourFeeSafe
export FEE_BPS=100

# Base NFT packs
export PAYMENT_TOKEN=0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913
export DEPLOY_721=true
export DEPLOY_20=false
forge script script/DeployFlashVRF.s.sol:DeployFlashVRF \
  --rpc-url https://mainnet.base.org --broadcast

# Robinhood ERC-20 packs
export PAYMENT_TOKEN=0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168
export DEPLOY_721=false
export DEPLOY_20=true
forge script script/DeployFlashVRF.s.sol:DeployFlashVRF \
  --rpc-url https://rpc.mainnet.chain.robinhood.com --broadcast
```

**ETH needed on RH:** ~**0.01–0.05 ETH** is a comfortable buffer for deploy + registration + initial fulfills (L2 is cheap; exact gas varies with L1 data fees).

## Deploy Phala Flash CVM

1. Use [Phala Cloud VRF template](https://cloud.phala.network/templates/vrf) or [GitHub template](https://github.com/Phala-Network/phala-cloud-vrf-template).
2. Env:
   - `RPC_URL` — Base or RH RPC (Helius/Alchemy preferred for reliability)
   - `CONTRACT_ADDRESS` — `PhalaFlashVRFCoordinator` address
3. After CVM is up:
   - `GET /get_wallet` → fund with **native ETH on that chain**
   - `GET /pubkey` → call `updateOffchainPublicKey(pubkeyAddress)` as owner
   - Optional: `setTrustedTEE(wallet)` for ops bookkeeping
4. Confirm CVM is subscribed to `RequestQueued` (event-driven fulfill).

> Note: Upstream template demos Base Sepolia / Abstract. RH is standard EVM — same binary, different RPC. Validate event polling against RH RPC before mainnet.

## End-to-end smoke test

1. Creator: mint/approve prizes → `createPack`
2. Buyer: approve payment → `buy(packId)` → note `purchaseId`, `vrfRequestId`
3. Wait ≤ ~10s for CVM fulfill (or check `getRandom(requestId)`)
4. If push enabled: prize already with buyer; else `settle(purchaseId)`
5. Creator: `claimProceeds()`
6. Failure path: stop CVM → wait `FULFILL_TIMEOUT` blocks → buyer `refund`

## Monitoring

| Signal | Alert if |
| --- | --- |
| TEE wallet ETH | Below ~0.001 ETH (chain-dependent) |
| Pending `RequestQueued` age | > 60s without `RandomFulfilled` |
| `CallbackFailed` events | Spike (push broken; pull still OK) |
| Escrow `reserved - sold` | Stuck pending grows unbounded |
| CVM health / attestation | Down or attestation expired |

## Incident playbooks

### CVM down

- Buyers can `refund` after `FULFILL_TIMEOUT` if no fulfill  
- If random already on-chain, `refund` **settles** (no free option)  
- Restart CVM; re-check `CONTRACT_ADDRESS` / RPC  

### Wrong pubkey registered

- Fulfills revert `InvalidSignature`  
- Owner: `updateOffchainPublicKey` to correct TEE pubkey  
- Pending requests need re-fulfill with new key (old sigs invalid)  

### Pause

- Escrow `pause()` blocks new buys/settles (owner)  
- Use only for security incidents; coordinate refunds  

## Security notes

- Transfer coordinator + escrow **ownership to multisig** before mainnet value  
- Never expose `UPDATE_SECRET_KEY_TOKEN` publicly  
- Publish attestation / CVM app id next to contract addresses  
- Do not reintroduce vault deposits for public inventory  

## Related

- [Randomness Architecture](randomness-architecture.md)
- [Vault Lifecycle](vault-lifecycle.md)
- Contracts README: `contracts/README.md`
