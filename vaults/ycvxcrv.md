# ycvxCRV Vault

The ycvxCRV vault accepts cvxCRV deposits and auto-compounds staking rewards from Convex Finance. ycvxCRV can be used as collateral on LlamaLend to borrow crvUSD. If you don't need collateral functionality, consider [yscvxCRV](yscvxcrv.md) for a lower fee.

## Overview

| Property | Value |
|----------|-------|
| Token | cvxCRV |
| Share Token | ycvxCRV |
| Vault Address | [0x95f19B19aff698169a1A0BBC28a2e47B14CB9a86](https://etherscan.io/address/0x95f19B19aff698169a1A0BBC28a2e47B14CB9a86) |
| Strategy Address | [0xCa960E6DF1150100586c51382f619efCCcF72706](https://etherscan.io/address/0xCa960E6DF1150100586c51382f619efCCcF72706) |
| Performance Fee | 20% (15% vault + 5% strategy) |
| Management Fee | 0% |

## How It Works

1. **Deposit** - Deposit cvxCRV and receive ycvxCRV vault shares
2. **Stake** - Your cvxCRV is staked on Convex Finance via the underlying strategy
3. **Harvest** - Anyone can call `report()` on the strategy to claim CRV, CVX, and crvUSD rewards
4. **Compound** - Anyone can call `kickAuction(token)` to swap a reward token (CRV, CVX, crvUSD) to cvxCRV for re-deposit
5. **Report** - Anyone can call `process_report()` on the vault to update accounting and collect fees for distribution to gauge
6. **Distribute** - Anyone can call `distribute()` on the accountant to send 15% fees to LlamaLend lenders
7. **Withdraw** - Redeem your ycvxCRV shares for cvxCRV plus accumulated yield

Harvesting and compounding are permissionless. Auctions only trigger when reward tokens exceed their `minAmountToSell` threshold (10 crvUSD). Use [CommonTrigger](https://etherscan.io/address/0xf8df17a35c88abb25e83c92f9d293b4368b9d52d) to check if thresholds are met. See [Permissionless Keeper](https://etherscan.io/address/0x52605bbf54845f520a3e94792d019f62407db2f8) for execution.

## LlamaLend Collateral

ycvxCRV can be used as collateral on [Curve LlamaLend](https://curve.finance/lend/#/ethereum/markets/one-way-market-35/) to borrow crvUSD. This allows you to:

- Earn yield on your cvxCRV
- Borrow against your position
- Maintain exposure while accessing liquidity

15% of the 20% performance fee on yield is distributed to LlamaLend lenders via a [Curve gauge](https://etherscan.io/address/0xa7B4B02953687Fd7f860bB6fE1c09450E01b8A71). The vault accountant periodically calls `distribute()` to send accumulated ycvxCRV to lenders who stake their lending vault shares in the gauge.

## Price Oracle

The LlamaLend market uses a price oracle based on Curve's [`CryptoFromPoolsRate`](https://docs.curve.finance/lending/contracts/cryptofrompoolsrate/) to value ycvxCRV collateral in crvUSD terms.

### Oracle Architecture

| Contract | Address | Description |
|----------|---------|-------------|
| Oracle Wrapper | [0xc1f1b19c870c06f322f397904EB46112650CE7eD](https://etherscan.io/address/0xc1f1b19c870c06f322f397904EB46112650CE7eD) | Combines pool oracle with vault pricePerShare |
| CryptoFromPoolsRate | [0xD7063E7e5EbF99b55c56F231f374F97C8578653a](https://etherscan.io/address/0xD7063E7e5EbF99b55c56F231f374F97C8578653a) | Chains cvxCRV -> CRV -> crvUSD price |

### How It Works

The oracle calculates the crvUSD value of ycvxCRV shares:

```
price = poolOracle.price() × vault.pricePerShare() / 1e18
```

Where:
- `poolOracle.price()` returns cvxCRV price in crvUSD (via Curve pool EMAs)
- `vault.pricePerShare()` returns cvxCRV per ycvxCRV share

### Price Path

The CryptoFromPoolsRate oracle chains two Curve pools:

1. **cvxCRV/CRV Pool** ([0x971add32Ea87f10bD192671630be3BE8A11b8623](https://etherscan.io/address/0x971add32Ea87f10bD192671630be3BE8A11b8623))
   - Returns cvxCRV price in CRV

2. **TriCRV Pool** ([0x4eBdF703948ddCEA3B11f675B4D1Fba9d2414A14](https://etherscan.io/address/0x4eBdF703948ddCEA3B11f675B4D1Fba9d2414A14))
   - Returns CRV price in crvUSD

### Safety Features

- **EMA Oracle** - Uses exponential moving average prices from Curve pools, not spot prices
- **Flash Loan Resistant** - EMA smoothing prevents single-block price manipulation
- **Battle-tested** - Built on Curve's production oracle infrastructure

### Governance

The LlamaLend market uses an oracle proxy ([0xcd22434e4c60042fb75916f57c3db91100bf5cad](https://etherscan.io/address/0xcd22434e4c60042fb75916f57c3db91100bf5cad)) that allows the Curve DAO (LlamaLend factory admin) to update the price oracle implementation if needed. This enables oracle upgrades without redeploying the market.

## Fee Structure

| Fee Type | Amount | Recipient |
|----------|--------|-----------|
| Vault Fee | 15% | LlamaLend lenders |
| Strategy Fee | 5% | yldfi |
| Management Fee | 0% | - |

Performance fees are only charged on profits, not on principal.

## Liquidation Risk

When using ycvxCRV as collateral on LlamaLend, you can borrow crvUSD against your position. Your collateral can be liquidated if its value drops significantly relative to your debt.

### Key Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Max LTV | **67%** | Maximum loan-to-value ratio at time of borrowing |
| Loan Discount | 33% | Buffer between collateral value and max borrowable amount |
| Liquidation Discount | 30% | Price discount at which soft liquidation begins |
| A (amplification) | 25 | Market parameter affecting band width |
| N (bands) | User-selected | Number of bands for your loan (more bands = more gradual liquidation) |
| AMM Fee | 0.6% | Fee charged during soft liquidation swaps |

### Understanding the Price Chain

The value of your ycvxCRV collateral depends on multiple factors:

```
ycvxCRV Price = pricePerShare × cvxCRV/CRV rate × CRV/USD price
```

cvxCRV trades at a discount to CRV on the secondary market. The discount can widen during market stress.

### How LLAMMA Liquidation Works

LlamaLend uses **soft liquidation** via the LLAMMA mechanism:

1. **Healthy Position**: Collateral value exceeds debt with sufficient margin
2. **Soft Liquidation Zone**: When price drops, your ycvxCRV gradually converts to crvUSD across your selected bands
3. **De-liquidation**: If price recovers, positions can convert back, though fees are incurred
4. **Hard Liquidation**: If health reaches 0, remaining position is fully liquidated

### Example Scenario

```
You deposit: 1000 ycvxCRV (worth ~309 crvUSD at current oracle price)
You borrow: 150 crvUSD (~48% LTV)

SCENARIO - cvxCRV discount widens:
─────────────────────────────────────────
Current cvxCRV/CRV: 0.44 (56% discount)
If discount widens to 70%: cvxCRV/CRV drops to ~0.30
→ Collateral value drops ~32%
→ Soft liquidation begins
→ ycvxCRV gradually converts to crvUSD

SCENARIO - CRV price drops:
─────────────────────────────────────────
If CRV/USD drops 40%:
→ ycvxCRV collateral value drops 40%
→ Combined with cvxCRV discount changes = compounded effect
```

### Risk Factors

- **cvxCRV Discount Volatility** - cvxCRV/CRV rate fluctuates based on market supply/demand
- **CRV Price Volatility** - CRV is subject to market price movements
- **Soft Liquidation Costs** - Conversions incur 0.6% AMM fee plus slippage

### Considerations

1. **N (Bands) Selection**: When creating a loan, you choose N. More bands spread liquidation across a wider price range; fewer bands concentrate it.
2. **cvxCRV/CRV Rate**: The [cvxCRV/CRV pool](https://curve.fi/#/ethereum/pools/factory-v2-22/swap) shows current market rates.
3. **Health Factor**: Visible in the LlamaLend UI when you have an active position.

### Market Contracts

| Contract | Address |
|----------|---------|
| Controller | [`0x24174143cCF438f0A1F6dCF93B468C127123A96E`](https://etherscan.io/address/0x24174143cCF438f0A1F6dCF93B468C127123A96E) |
| AMM (LLAMMA) | [`0xF1b03586c03EBfEC014238D105148A15102A282f`](https://etherscan.io/address/0xF1b03586c03EBfEC014238D105148A15102A282f) |
| Lending Vault | [`0xe5Ee62F37825EEd77215c9D2e9d424B79C62124a`](https://etherscan.io/address/0xe5Ee62F37825EEd77215c9D2e9d424B79C62124a) |
| Price Oracle | [`0xcd22434e4c60042fb75916f57c3db91100bf5cad`](https://etherscan.io/address/0xcd22434e4c60042fb75916f57c3db91100bf5cad) |
