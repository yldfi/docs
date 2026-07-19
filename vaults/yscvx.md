# ysCVX Strategy

The ysCVX strategy accepts [CVX](https://etherscan.io/address/0x4e3FBD56CD56c3e72c1403e103b45Db9da5B9D2B) deposits and auto-compounds staking rewards from [Convex Finance](https://www.convexfinance.com). This is a standalone Yearn V3 tokenized strategy that is fully ERC-4626 compliant.

## Overview

| Property | Value |
|----------|-------|
| Token | CVX |
| Share Token | ysCVX |
| Contract Address | [0x1Fd0A85084fC61c397AC619c4F0bA2350eA1cE9e](https://etherscan.io/address/0x1Fd0A85084fC61c397AC619c4F0bA2350eA1cE9e) |
| Contract Type | Yearn V3 Tokenized Strategy (ERC-4626) |
| Performance Fee | 5% |
| Management Fee | 0% |
| Profit Unlock Time | 10 days |

## How It Works

1. **Deposit** - Deposit CVX and receive ysCVX shares
2. **Stake** - Your CVX is staked on Convex Finance's [cvxRewardPool](https://etherscan.io/address/0xCF50b810E57Ac33B91dCF525C6ddd9881B139332)
3. **Harvest** - Anyone can call `report()` on the strategy to claim cvxCRV rewards
4. **Compound** - Anyone can call `kickAuction(cvxCRV)` to auction off cvxCRV rewards for more CVX for re-deposit
5. **Withdraw** - Redeem your ysCVX shares for CVX plus accumulated yield

Harvesting and compounding are permissionless. Use the [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) to `report()` rewards on the strategy.

## Fee Structure

| Fee Type | Amount | Recipient |
|----------|--------|-----------|
| Performance Fee | 5% | [yld Multisig](https://etherscan.io/address/0x8baecb301FD723Ff35FB1D9a6d595cAD35618A6f) |
| Management Fee | 0% | - |

Performance fees are only charged on profits, not on principal.

## Key Contracts

| Contract | Address |
|----------|---------|
| CVX Token | [0x4e3FBD56CD56c3e72c1403e103b45Db9da5B9D2B](https://etherscan.io/address/0x4e3FBD56CD56c3e72c1403e103b45Db9da5B9D2B) |
| cvxCRV Token (reward) | [0x62B9c7356A2Dc64a1969e19C23e4f579F9810Aa7](https://etherscan.io/address/0x62B9c7356A2Dc64a1969e19C23e4f579F9810Aa7) |
| Convex cvxRewardPool | [0xCF50b810E57Ac33B91dCF525C6ddd9881B139332](https://etherscan.io/address/0xCF50b810E57Ac33B91dCF525C6ddd9881B139332) |
