# Token Launch

Token and registry work can proceed **independently** of the reduced analysis scope — but **must not** over-promise pack economics.

## Current Principle

1. Launch agents with a narrow, reliable service surface first:
   - Miss: randomness + Pokemon data/analysis  
   - OpenClawMachine: cross-game graded comps and analysis  
2. Expand token-linked revenue only after transactional services are live **on-chain**.

## Robinhood Chain deployment (planned)

| Item | Intent |
| --- | --- |
| Chain | Robinhood Chain mainnet `4663` (testnet `46630` first) |
| Contract | `ClawMachineToken` — fixed supply ERC-20, mint once to treasury |
| Symbol | `CLAWMACHINE` (confirm before mainnet) |
| Treasury | **Multisig only** on mainnet |
| Utility (later) | Brand, optional fee discounts, governance — TBD in writing before mainnet |

### Not claims

- Not a share of Beezie/CC inventory  
- Not redeemable for physical cards  
- Not a guarantee of pack platform revenue  

## Relationship to packs

Pack fees (1%) accrue in **USDC/USDG** to fee recipients configured on escrow contracts. Any link from those fees to the token must be a separate, documented policy.

## Before mainnet mint checklist

- [ ] Multisig treasury address published  
- [ ] Tokenomics one-pager reviewed  
- [ ] Testnet deploy + verify on Blockscout  
- [ ] Narrative page still matches live status  

See [Product Narrative](narrative.md) and `contracts/src/ClawMachineToken.sol`.
