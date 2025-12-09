# yscvgCVX Vault

The yscvgCVX vault accepts [cvgCVX](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) deposits and auto-compounds staking rewards from [Tangent Finance's LiquidBoost](https://docs-liquidboost.tangent.finance/liquidboost) program.

## Overview

| Property | Value |
|----------|-------|
| Token | cvgCVX |
| Share Token | yscvgCVX |
| Vault Address | [0x0849b046292293f78dF3002F8461f8A7e2eC2b82](https://etherscan.io/address/0x0849b046292293f78dF3002F8461f8A7e2eC2b82) |
| Strategy Address | [0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359](https://etherscan.io/address/0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359) |
| Contract Type | Yearn V3 Tokenized Strategy (ERC-4626) |
| Performance Fee | 5% |
| Management Fee | 0% |
| Profit Unlock Time | 14 days |

## What is cvgCVX?

[cvgCVX](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) is a liquid wrapper for CVX created by [Tangent Finance's LiquidBoost](https://docs-liquidboost.tangent.finance/liquidboost). It allows users to earn CVX voting incentives without locking their capital.

## How It Works

1. **Deposit** - Deposit cvgCVX and receive yscvgCVX vault shares
2. **Stake** - Your cvgCVX is staked in the Tangent [LiquidBoost staking contract](https://etherscan.io/address/0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119)
3. **Harvest** - Anyone can call `report()` on the strategy to claim cvgCVX rewards and restake them
4. **Withdraw** - Redeem your yscvgCVX shares for cvgCVX plus accumulated yield

Rewards are paid in cvgCVX (the same token as the deposit), so no swaps or auctions are needed. This keeps the strategy simple, gas-efficient, and free of slippage risk.

## Reward Cycle

LiquidBoost operates on a weekly cycle schedule. Rewards follow an N+2 delay:

| Cycle | Status |
|-------|--------|
| N (deposit) | Pending — not yet earning |
| N+1 | Active — accruing rewards (must stay staked entire cycle) |
| N+2 | Rewards claimable |

Minimum time from deposit to first reward claim is approximately **14 days**. The strategy's profit unlock time is set to 14 days to align with this cycle.

## Fee Structure

| Fee Type | Amount | Recipient |
|----------|--------|-----------|
| Performance Fee | 5% | [yld Multisig](https://etherscan.io/address/0x8baecb301FD723Ff35FB1D9a6d595cAD35618A6f) |
| Management Fee | 0% | - |

Performance fees are only charged on profits, not on principal.

## Key Contracts

| Contract | Address |
|----------|---------|
| cvgCVX Token | [0x2191DF768ad71140F9F3E96c1e4407A4aA31d082](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) |
| Tangent Staking (LiquidBoost) | [0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119](https://etherscan.io/address/0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119) |
