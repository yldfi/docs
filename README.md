# yld

yld provides automated yield vaults on Ethereum built on [Yearn V3 yVault technology](https://docs.yearn.fi/getting-started/products/yvaults/v3), following the ERC-4626 standard. Deposit your tokens and earn auto-compounding returns without manual intervention.

## Available Vaults

| Vault                          | Token  | Strategy                       | Fee                                  | LlamaLend Collateral |
| ------------------------------ | ------ | ------------------------------ | ------------------------------------ | -------------------- |
| [ycvxCRV](vaults/ycvxcrv.md)   | cvxCRV | Convex auto-compounder         | 20% (15% LlamaLend Lenders + 5% yld) | Yes                  |
| [yscvxCRV](vaults/yscvxcrv.md) | cvxCRV | Convex auto-compounder         | 5% (yld)                             | No                   |
| [yscvgCVX](vaults/yscvgcvx.md) | cvgCVX | Tangent LiquidBoost compounder | 5% (yld)                             | No                   |

## Quick Links

* [Website](https://yldfi.co)
* [X.com](https://x.com/yld_fi)
* [GitHub](https://github.com/yldfi)
* [Telegram](https://t.me/yld_official)
* [Contracts](contracts/addresses.md)
