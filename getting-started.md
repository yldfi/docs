# Getting Started

This guide will walk you through depositing into a yldfi vault.

## Prerequisites

- An Ethereum wallet (MetaMask, Rainbow, etc.)
- [cvxCRV](https://etherscan.io/token/0x62B9c7356A2Dc64a1969e19C23e4f579F9810Aa7) tokens
- ETH for gas fees

## How to Obtain cvxCRV

### Option 1: Buy on Curve (Recommended)

Swap any token for cvxCRV on Curve:

1. Go to [Curve cvxCRV/CRV Pool](https://curve.fi/#/ethereum/pools/factory-v2-22/swap)
2. Select your input token (ETH, CRV, USDC, etc.)
3. Set cvxCRV as output
4. Approve and swap

This is typically the best option as cvxCRV trades at a discount to CRV.

### Option 2: Convert CRV to cvxCRV

If you hold CRV, you can convert it 1:1 to cvxCRV via Convex:

1. Go to [Convex Finance](https://www.convexfinance.com/stake)
2. Navigate to "CRV" → "Convert to cvxCRV"
3. Enter amount and confirm

> **Note**: This conversion is one-way at the protocol level. Once CRV is converted to cvxCRV, it cannot be redeemed back 1:1. You can only sell cvxCRV on the secondary market, typically at a discount.

### Which Option?

| Method | When to Use |
|--------|-------------|
| Buy on Curve | cvxCRV is trading below 1:1 with CRV (usually the case) |
| Convert via Convex | cvxCRV is trading at or above 1:1 with CRV (rare) |

Check the current rate on the [cvxCRV/CRV pool](https://curve.fi/#/ethereum/pools/factory-v2-22/swap) before deciding.

## Step 1: Connect Your Wallet

1. Go to [yldfi.co](https://yldfi.co)
2. Click **Connect** in the top right
3. Select your wallet and approve the connection
4. Make sure you're on **Ethereum mainnet**

## Step 2: Choose a Vault

yldfi offers two cvxCRV vaults:

| Vault | Fee | LlamaLend Collateral |
|-------|-----|---------------------|
| [ycvxCRV](vaults/ycvxcrv.md) | 20% (15% to LlamaLend lenders + 5% strategy) | Yes |
| [yscvxCRV](vaults/yscvxcrv.md) | 5% | No |

**ycvxCRV** - Best if you want to borrow against your position on LlamaLend. The higher 20% fee exists because 15% is distributed to LlamaLend lenders to encourage borrowing liquidity.

**yscvxCRV** - Best if you want maximum yield with the lowest 5% fee. Cannot be used as LlamaLend collateral.

## Step 3: Approve & Deposit

1. Click on your chosen vault
2. Enter the amount of cvxCRV to deposit
3. Click **Approve** (first time only)
4. Confirm the approval in your wallet
5. Click **Deposit**
6. Confirm the deposit in your wallet

## Step 4: Earn Yield

That's it! Your cvxCRV is now earning auto-compounded yield. You can:

- View your position value on the vault page
- Withdraw anytime by clicking **Withdraw**
- Use ycvxCRV as collateral on [LlamaLend](https://curve.finance/lend/#/ethereum/markets/one-way-market-35/)

## Where Does the Yield Come From?

1. Your cvxCRV is staked on Convex Finance via a wrapper contract
2. Staking earns CRV, CVX, and crvUSD rewards
3. Anyone can call `report()` on the strategy to harvest rewards
4. Anyone can call `kickAuction(token)` to swap reward tokens (CRV, CVX, crvUSD) to cvxCRV via dutch auction
5. cvxCRV is re-staked to compound your position
6. For ycvxCRV, `process_report()` on the vault calculates fees, then `distribute()` on the accountant sends 15% to LlamaLend lenders
7. Your vault shares represent your growing cvxCRV balance

yldfi runs a keeper bot to automatically call these functions when thresholds are met. Anyone can also call them permissionlessly using [CommonTrigger](https://etherscan.io/address/0xf8df17a35c88abb25e83c92f9d293b4368b9d52d) to check if minimum thresholds are ready.
