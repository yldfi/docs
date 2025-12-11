# Security

Don't Trust, Verify.

All contracts are:

- **Immutable** - Management has been renounced; no one can change parameters or upgrade contracts
- **Non-custodial** - Users retain control of funds at all times
- **Open source** - Code available on [GitHub](https://github.com/yldfi) and verified on [Etherscan](https://etherscan.io)
- **Built on Yearn V3** - Based on the audited Yearn V3 tokenized strategy architecture ([audits](https://github.com/yearn/yearn-vaults-v3/tree/master/audits))

## Audit Status

### Yearn V3 Foundation

yldfi vaults are built on Yearn V3's tokenized strategy architecture, which has been professionally audited. Yearn V3 audit reports are available in the [Yearn GitHub repository](https://github.com/yearn/yearn-vaults-v3/tree/master/audits).

### yldfi Implementation

The yldfi-specific contracts have **not been independently audited** as the strategies are intentionally simple and minimal:

- **No novel logic**: Deposits go directly to Convex staking; withdrawals pull from Convex. No complex routing, leverage, or cross-protocol interactions.
- **Standard integrations**: Uses battle-tested Convex and Curve contracts that have been live for years with billions in TVL.
- **Yearn's audited base**: The TokenizedStrategy core (share accounting, ERC-4626 compliance, fee logic) is inherited directly from Yearn V3's audited code—yldfi doesn't modify these internals.
- **Permissionless operations**: Harvesting and compounding can be called by anyone; no privileged keeper logic.
- **Immutable deployment**: Management has been renounced. No admin functions that could alter vault behavior post-deployment.

The yldfi-specific code is primarily configuration: which token to stake, where to stake it, and how to swap rewards back. The heavy lifting is done by audited Yearn, Convex, and Curve contracts.

## Risks

DeFi always carries risks. Never deposit more than you can afford to lose.

- **Smart Contract Risk** - Bugs may exist despite audited foundations
- **Underlying Protocol Risk** - yldfi depends on Convex and Curve

## Contract Verification

All contracts are verified on Etherscan. See [Contract Addresses](contracts/addresses.md) for the full list.

## Disclaimer

Yearn Finance does not endorse, audit, or maintain yldfi vaults.
