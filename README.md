# yld

yld provides automated yield vaults on Ethereum built on [Yearn V3 yVault technology](https://docs.yearn.fi/getting-started/products/yvaults/v3), following the ERC-4626 standard. Deposit your tokens and earn auto-compounding returns without manual intervention.

## Available Vaults

| Vault                                                | Token  | Strategy                       | Fee                                  | LlamaLend Collateral |
| ----------------------------------------------------- | ------ | ------------------------------ | ------------------------------------ | -------------------- |
| [yscvxCRV](vaults/yscvxcrv.md)                        | cvxCRV | Convex auto-compounder         | 5% (yld)                             | No                   |
| [ysCVX](vaults/yscvx.md)                              | CVX    | Convex auto-compounder         | 5% (yld)                             | No                   |

## Sunset Vaults

These vaults no longer accept new deposits through yld.

| Vault                                 | Token  | Status                                                    | Reason                                                     |
| ------------------------------------- | ------ | --------------------------------------------------------- | ---------------------------------------------------------- |
| [ycvxCRV](vaults/ycvxcrv.md)          | cvxCRV | Exit-only: withdrawals and existing LlamaLend loans only | Curve DAO is sunsetting the LlamaLend v1 market            |
| [ycvgCVX](vaults/yscvgcvx.md)         | cvgCVX | Fully withdrawn, removed from the app                     | Tangent has deprecated cvgCVX and LiquidBoost              |
| [yscvgCVX](vaults/yscvgcvx.md)        | cvgCVX | Fully withdrawn, removed from the app                     | Tangent has deprecated cvgCVX and LiquidBoost              |

ycvxCRV holders should exchange to [yscvxCRV](vaults/yscvxcrv.md) to keep earning on their cvxCRV.

## Quick Links

* [Website](https://yldfi.co)
* [X.com](https://x.com/yld_fi)
* [GitHub](https://github.com/yldfi)
* [Telegram](https://t.me/yld_official)
* [Contracts](contracts/addresses.md)
