# yld

yld provides automated yield vaults on Ethereum built on [Yearn V3 yVault technology](https://docs.yearn.fi/getting-started/products/yvaults/v3), following the ERC-4626 standard. Deposit your tokens and earn auto-compounding returns without manual intervention.

## Available Vaults

| Vault                                                | Token  | Strategy                       | Fee                                  | LlamaLend Collateral |
| ----------------------------------------------------- | ------ | ------------------------------ | ------------------------------------ | -------------------- |
| [yscvxCRV](vaults/yscvxcrv.md)                        | cvxCRV | Convex auto-compounder         | 5% (yld)                             | No                   |
| [ysCVX](vaults/yscvx.md)                              | CVX    | Convex auto-compounder         | 5% (yld)                             | No                   |

## Sunset Vaults

| Vault    | Token  | Reason                                                                                                                                                         |
| -------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ycvxCRV  | cvxCRV | Curve DAO is sunsetting the LlamaLend v1 market ([forum post](https://gov.curve.finance/t/llamalend-v1-market-deprecation-plan/11075))                        |
| ycvgCVX  | cvgCVX | LiquidBoost has sunset cvgCVX ([Tangent proposal](https://snapshot.box/#/s:tangent-finance.eth/proposal/0xc3191a83f52633262942c2a239af278b0b5e17c506c6e9894ee3b38dd95012a1)) |
| yscvgCVX | cvgCVX | LiquidBoost has sunset cvgCVX ([Tangent proposal](https://snapshot.box/#/s:tangent-finance.eth/proposal/0xc3191a83f52633262942c2a239af278b0b5e17c506c6e9894ee3b38dd95012a1)) |

## Quick Links

* [Website](https://yldfi.co)
* [X.com](https://x.com/yld_fi)
* [GitHub](https://github.com/yldfi)
* [Telegram](https://t.me/yld_official)
* [Contracts](contracts/addresses.md)
