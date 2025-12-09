# yscvxCRV Strategy

The yscvxCRV strategy accepts [cvxCRV](https://etherscan.io/address/0x62B9c7356A2Dc64a1969e19C23e4f579F9810Aa7) deposits and auto-compounds staking rewards from [Convex Finance](https://www.convexfinance.com) with a lower fee structure. This is a standalone Yearn V3 tokenized strategy that is fully ERC-4626 compliant.

## Overview

| Property | Value |
|----------|-------|
| Token | cvxCRV |
| Share Token | yscvxCRV |
| Contract Address | [0xCa960E6DF1150100586c51382f619efCCcF72706](https://etherscan.io/address/0xCa960E6DF1150100586c51382f619efCCcF72706) |
| Contract Type | Yearn V3 Tokenized Strategy (ERC-4626) |
| Performance Fee | 5% |
| Management Fee | 0% |
| Profit Unlock Time | 3 days |

## How It Works

1. **Deposit** - Deposit cvxCRV and receive yscvxCRV shares
2. **Stake** - Your cvxCRV is staked on [Convex Finance](https://www.convexfinance.com)
3. **Harvest** - Anyone can call `report()` on the strategy to claim CRV, CVX, and crvUSD rewards
4. **Compound** - Anyone can call `kickAuction(token)` to auction off rewards for more underlying asset (cvxCRV) for re-deposit
5. **Withdraw** - Redeem your yscvxCRV shares for cvxCRV plus accumulated yield

Harvesting and compounding are permissionless. Auctions only trigger when reward tokens exceed their `minAmountToSell` threshold (10 crvUSD). Use the [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) to `report()` rewards on the strategy.

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
| Performance Fee | 5% | [yld Multisig](https://etherscan.io/address/0x8baecb301FD723Ff35FB1D9a6d595cAD35618A6f) |
| Management Fee | 0% | - |

Performance fees are only charged on profits, not on principal.
