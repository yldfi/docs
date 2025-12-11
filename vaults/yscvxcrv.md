# yscvxCRV Strategy

The yscvxCRV strategy accepts cvxCRV deposits and auto-compounds staking rewards from Convex Finance with a lower fee structure. This is a standalone Yearn V3 tokenized strategy that is fully ERC-4626 compliant.

## Overview

| Property | Value |
|----------|-------|
| Token | cvxCRV |
| Share Token | yscvxCRV |
| Contract Address | [0xCa960E6DF1150100586c51382f619efCCcF72706](https://etherscan.io/address/0xCa960E6DF1150100586c51382f619efCCcF72706) |
| Contract Type | Yearn V3 Tokenized Strategy (ERC-4626) |
| Performance Fee | 5% |
| Management Fee | 0% |

## How It Works

1. **Deposit** - Deposit cvxCRV and receive yscvxCRV shares
2. **Stake** - Your cvxCRV is staked on Convex Finance
3. **Harvest** - Anyone can call `report()` on the strategy to claim CRV, CVX, and crvUSD rewards
4. **Compound** - Anyone can call `kickAuction(token)` to swap a reward token (CRV, CVX, crvUSD) to cvxCRV for re-deposit
5. **Withdraw** - Redeem your yscvxCRV shares for cvxCRV plus accumulated yield

Harvesting and compounding are permissionless. Auctions only trigger when reward tokens exceed their `minAmountToSell` threshold (10 crvUSD). Use [CommonTrigger](https://etherscan.io/address/0xf8df17a35c88abb25e83c92f9d293b4368b9d52d) to check if thresholds are met. See [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) for execution.

## Differences from ycvxCRV

| Feature | ycvxCRV | yscvxCRV |
|---------|---------|----------|
| Performance Fee | 20% (15% to LlamaLend lenders + 5% strategy) | 5% |
| LlamaLend Collateral | Yes | No |
| Contract Type | Vault + Strategy | Strategy only |

yscvxCRV has a lower fee but cannot be used as collateral on LlamaLend. The ycvxCRV vault has a higher fee because 15% of the 20% is distributed to LlamaLend lenders to encourage borrowing liquidity.

## Fee Structure

| Fee Type | Amount | Recipient |
|----------|--------|-----------|
| Performance Fee | 5% | yldfi |
| Management Fee | 0% | - |

Performance fees are only charged on profits, not on principal.
