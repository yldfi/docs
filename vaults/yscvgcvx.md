# ycvgCVX & yscvgCVX (Sunset)

> ⛔ **Sunset** — Tangent has deprecated cvgCVX and its [LiquidBoost](https://docs-liquidboost.tangent.finance/liquidboost) program, so yld has sunset its cvgCVX products. All cvgCVX has been withdrawn from ycvgCVX and yscvgCVX, and both have been removed from the yld app. The contracts stay on-chain, but the vaults no longer accept deposits through yld and are no longer harvested. This page is kept for reference.
>
> To keep earning with yld, see [yscvxCRV](yscvxcrv.md) or [ysCVX](yscvx.md).

The yscvgCVX strategy accepted [cvgCVX](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) deposits and auto-compounded staking rewards from [Tangent Finance's LiquidBoost](https://docs-liquidboost.tangent.finance/liquidboost) program. ycvgCVX was a meta-vault on top of the yscvgCVX strategy. It was only reachable through zaps in the yld app and was never listed as a separate vault.

## Overview

| Property | Value |
|----------|-------|
| Status | Sunset (October 2026) |
| Token | cvgCVX |
| Share Tokens | ycvgCVX (vault), yscvgCVX (strategy) |
| ycvgCVX Vault Address | [0x0849b046292293f78dF3002F8461f8A7e2eC2b82](https://etherscan.io/address/0x0849b046292293f78dF3002F8461f8A7e2eC2b82) |
| yscvgCVX Strategy Address | [0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359](https://etherscan.io/address/0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359) |
| Contract Type | Yearn V3 Vault / Tokenized Strategy (ERC-4626) |
| Performance Fee | 5% |
| Management Fee | 0% |
| Profit Unlock Time | 14 days |

## What was cvgCVX?

[cvgCVX](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) was a liquid wrapper for CVX created by [Tangent Finance's LiquidBoost](https://docs-liquidboost.tangent.finance/liquidboost). It let holders earn CVX voting incentives without locking their capital.

## How It Worked

1. **Deposit** - Deposit cvgCVX and receive yscvgCVX shares (or ycvgCVX shares via the meta-vault)
2. **Stake** - The cvgCVX was staked in the Tangent [LiquidBoost staking contract](https://etherscan.io/address/0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119)
3. **Harvest** - Anyone could call `report()` on the strategy to claim cvgCVX rewards and restake them
4. **Withdraw** - Redeem shares for cvgCVX plus accumulated yield

Rewards were paid in cvgCVX (the same token as the deposit), so no swaps or auctions were needed.

## Reward Cycle

LiquidBoost operated on a weekly cycle schedule. Rewards followed an N+2 delay:

| Cycle | Status |
|-------|--------|
| N (deposit) | Pending — not yet earning |
| N+1 | Active — accruing rewards (must stay staked entire cycle) |
| N+2 | Rewards claimable |

The minimum time from deposit to first reward claim was approximately **14 days**, so the strategy's profit unlock time was set to 14 days to match.

## Fee Structure

| Fee Type | Amount | Recipient |
|----------|--------|-----------|
| Performance Fee | 5% | [yld Multisig](https://etherscan.io/address/0x8baecb301FD723Ff35FB1D9a6d595cAD35618A6f) |
| Management Fee | 0% | - |

## Key Contracts

| Contract | Address |
|----------|---------|
| ycvgCVX Vault | [0x0849b046292293f78dF3002F8461f8A7e2eC2b82](https://etherscan.io/address/0x0849b046292293f78dF3002F8461f8A7e2eC2b82) |
| yscvgCVX Strategy | [0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359](https://etherscan.io/address/0x8ED5AB1BA2b2E434361858cBD3CA9f374e8b0359) |
| cvgCVX Token | [0x2191DF768ad71140F9F3E96c1e4407A4aA31d082](https://etherscan.io/address/0x2191DF768ad71140F9F3E96c1e4407A4aA31d082) |
| Tangent Staking (LiquidBoost) | [0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119](https://etherscan.io/address/0x2c1D293c50C6d1a4370ebb442A02c5956bbAb119) |
