# FAQ

## General

### What is yld?

yld provides automated yield vaults on Ethereum. Deposit tokens and earn auto-compounding returns without manual intervention.

### Is yld safe?

See [Security](security.md) for details on immutability, non-custodial design, open source code, and audit status. DeFi always carries risks.

Performance fees are only charged on profits, not principal.

## Vaults & Strategies

### What's the difference between "y" and "ys" vaults?

All vaults are ERC-4626 compliant and auto-compound rewards.

**"y" vaults** (e.g. ycvxCRV) are wrapper vaults that can be used as **collateral on LlamaLend**. They have a higher fee because a portion is distributed to LlamaLend lenders to encourage borrowing liquidity.

**"ys" vaults** (e.g. yscvxCRV, ysCVX) are the underlying strategies that can be deposited into directly. They have **lower fees** but cannot be used as LlamaLend collateral.

| Vault    | Type          | Token  | LlamaLend Collateral |
| -------- | ------------- | ------ | -------------------- |
| ycvxCRV  | y (vault)     | cvxCRV | Yes                  |
| yscvxCRV | ys (strategy) | cvxCRV | No                   |
| ysCVX    | ys (strategy) | CVX    | No                   |

### Can I withdraw anytime?

Yes. There are no lockups or withdrawal fees. You can redeem your shares for underlying tokens at any time.&#x20;

### How often are rewards compounded?

yld runs a keeper bot to automatically compound rewards when profit unlock times are met. Compounding is also permissionless and involves two steps:

1. **Report** - Call `process_report()` on the vault (eg. ycvxCRV) or `report()` on the strategy (eg. yscvxCRV) via the [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) to harvest rewards
2. **Auction** - Call `kickAuction()` on the strategy to auction off rewards for more underlying asset (cvxCRV) for re-deposit

The [CommonTrigger](https://etherscan.io/address/0xf8df17a35c88abb25e83c92f9d293b4368b9d52d) contract provides view functions to check when reports and auctions should be triggered.

### What is the exchange rate?

Vault shares appreciate over time relative to the underlying token. 1 ycvxCRV will always be redeemable for more than 1 cvxCRV (after yield accrues).

## LlamaLend

### What is LlamaLend?

LlamaLend is Curve's lending platform. You can deposit ycvxCRV as collateral and borrow crvUSD against it.

### Why can't I use yscvxCRV as collateral?

ycvxCRV was specifically deployed on LlamaLend because it includes functionality to redistribute 15% of yield fees to LlamaLend lenders. This deepens liquidity and reduces borrowing rates. yscvxCRV doesn't have this fee redistribution mechanism.
