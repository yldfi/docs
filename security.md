# Security

Don't Trust, Verify.

All contracts are:

- **Non-custodial** - Users retain control of funds at all times
- **Open source** - Code available on [GitHub](https://github.com/yldfi) and verified on [Etherscan](https://etherscan.io)
- **Built on Yearn V3** - Based on the audited Yearn V3 tokenized strategy architecture ([audits](https://github.com/yearn/yearn-vaults-v3/tree/master/audits))

Select contracts have been made **immutable** via [NullGovernance](#immutability).

## Audit Status

### Yearn V3 Foundation

yld vaults are built on Yearn V3's tokenized strategy architecture, which has been professionally audited. Yearn V3 audit reports are available in the [Yearn GitHub repository](https://github.com/yearn/yearn-vaults-v3/tree/master/audits).

### yld Implementation

The yld-specific contracts have **not been independently audited** as the strategies are intentionally simple and minimal:

- **No novel logic**: Deposits go directly to Convex staking; withdrawals pull from the respective protocol. No complex routing, leverage, or cross-protocol interactions.
- **Standard integrations**: Uses battle-tested Convex and Curve contracts that have been live for years with billions in TVL.
- **Yearn's audited base**: The TokenizedStrategy core (share accounting, ERC-4626 compliance, fee logic) is inherited directly from Yearn V3's audited code—yld doesn't modify these internals.
- **Permissionless operations**: Harvesting and compounding can be called by anyone; no privileged keeper logic.
- **Governance renunciation**: ycvxCRV and yscvxCRV have been made permanently immutable via [NullGovernance](#immutability).

The yld-specific code is primarily configuration: which token to stake, where to stake it, and how to swap rewards back. The heavy lifting is done by audited Yearn, Convex, and Curve contracts.

## Immutability

Governance and administration of select yld contracts has been permanently transferred to [NullGovernance](https://etherscan.io/address/0x99f23ae4ab2f3dc5b6b093d1729dbadabd3f29cd).

NullGovernance is a stateless, permissionless contract that serves as a dead-end ownership sink. It contains only `accept*` functions — it can accept management, role manager, governance, and fee manager roles from Yearn V3 contracts. Critically, it has **no functions to exercise any of those roles**: no ability to change fees, swap strategies, set parameters, transfer ownership further, or call any privileged operation on the managed contracts.

Once a contract's ownership is transferred to NullGovernance, the change is **irreversible** — there is no mechanism to transfer ownership back out. This makes the source contract permanently immutable.

### Immutable Contracts

The following contracts are governed by NullGovernance:

- ycvxCRV Vault
- yscvxCRV Strategy

### Managed Contracts

The following contracts are currently managed by the [yld Multisig](https://etherscan.io/address/0x8baecb301FD723Ff35FB1D9a6d595cAD35618A6f):

- yscvgCVX Strategy (sunset)

## Risks

DeFi always carries risks. Never deposit more than you can afford to lose.

- **Smart Contract Risk** - Bugs may exist despite audited foundations
- **Underlying Protocol Risk** - yld depends on Convex and Curve

## Contract Verification

All contracts are verified on Etherscan. See [Contract Addresses](contracts/addresses.md) for the full list.

## Disclaimer

**Use at your own risk.** yld is provided "as is" without warranties of any kind, express or implied. The developers and contributors accept no liability for any loss of funds, damages, or other consequences arising from the use of yld vaults or any associated smart contracts. You are solely responsible for your own financial decisions.

By using yld, you acknowledge that:

- DeFi protocols involve inherent risks including but not limited to smart contract bugs, oracle failures, liquidity risks, and regulatory uncertainty
- Past performance does not guarantee future results
- You should never deposit more than you can afford to lose
- You have read and agree to the [Terms and Conditions](https://yldfi.co/terms)

Yearn Finance does not endorse, audit, or maintain yld vaults.
