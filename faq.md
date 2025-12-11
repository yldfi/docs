# FAQ

## General

### What is yldfi?

yldfi provides automated yield vaults on Ethereum. Deposit tokens and earn auto-compounding returns without manual intervention.

### Is yldfi safe?

See [Security](security.md) for details on immutability, non-custodial design, open source code, and audit status. DeFi always carries risks.

### What are the fees?

| Vault | Performance Fee | Management Fee |
|-------|-----------------|----------------|
| ycvxCRV | 20% (15% to LlamaLend lenders + 5% strategy) | 0% |
| yscvxCRV | 5% | 0% |

Performance fees are only charged on profits, not principal.

## Vaults & Strategies

### What's the difference between ycvxCRV and yscvxCRV?

Both are ERC-4626 vaults that auto-compound cvxCRV rewards:

- **ycvxCRV** - Can be used as collateral on LlamaLend. 20% performance fee (15% distributed to LlamaLend lenders to encourage borrowing liquidity + 5% strategy fee)
- **yscvxCRV** - Lower 5% fee, but no LlamaLend collateral support

### Can I withdraw anytime?

Yes. There are no lockups or withdrawal fees. You can redeem your shares for underlying tokens at any time.

### How often are rewards compounded?

yldfi runs a keeper bot to automatically compound rewards when thresholds are met. Compounding is also permissionless and involves two steps:

1. **Report** - Call `process_report()` on the vault (ycvxCRV) or `report()` on the strategy (yscvxCRV) via the [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) to harvest rewards (CRV, CVX, crvUSD)
2. **Auction** - Call `kickAuction()` on the strategy to swap harvested rewards to cvxCRV for re-deposit

The [CommonTrigger](https://etherscan.io/address/0xf8df17a35c88abb25e83c92f9d293b4368b9d52d) contract provides view functions to check when reports and auctions should be triggered.

### What is the exchange rate?

Vault shares appreciate over time relative to the underlying token. 1 ycvxCRV will always be redeemable for more than 1 cvxCRV (after yield accrues).

## LlamaLend

### What is LlamaLend?

LlamaLend is Curve's lending platform. You can deposit ycvxCRV as collateral and borrow crvUSD against it.

### Why can't I use yscvxCRV as collateral?

ycvxCRV was specifically deployed on LlamaLend because it includes functionality to redistribute 15% of yield fees to LlamaLend lenders. This deepens liquidity and reduces borrowing rates. yscvxCRV doesn't have this fee redistribution mechanism.
