---
description: Smart contract addresses for Euler
---

# Addresses

Besides Euler, the smart contracts are upgradeable via Governance which will be controlled by EUL token holders (i.e., the implementation contracts will be upgraded periodically). Hence, for contract interaction, please use the proxy smart contract addresses.

For example, using [web3.js](https://web3js.readthedocs.io/en/v1.2.11/web3-eth-contract.html) to interact with the Markets contract, we use the Markets contract ABI but set the Markets contract proxy address as the target contract:

```javascript
const markets = new Contract(MarketsABI, Markets_Proxy_Address); // proxy address
```

## Networks
The Euler protocol is currently deployed to the following networks:


### Mainnet

| Contract | Proxy Address | Etherscan (Proxy) | Etherscan (Implementation) | Source Code |
|-------|------|------|------|------|
| Euler | 0x27182842E098f60e3D576794A5bFFb0777E025d3 | | [Etherscan](https://etherscan.io/address/0x27182842E098f60e3D576794A5bFFb0777E025d3) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/Euler.sol) |
| Markets | 0x3520d5a913427E6F0D6A83E07ccD4A4da316e4d3 | [Etherscan](https://etherscan.io/address/0x3520d5a913427E6F0D6A83E07ccD4A4da316e4d3) | [Etherscan](https://etherscan.io/address/0xE5d0A7A3ad358792Ba037cB6eE375FfDe7Ba2Cd1) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Markets.sol) |
| Liquidation | 0xf43ce1d09050BAfd6980dD43Cde2aB9F18C85b34 | [Etherscan](https://etherscan.io/address/0xf43ce1d09050BAfd6980dD43Cde2aB9F18C85b34) | [Etherscan](https://etherscan.io/address/0xAed37a234cc880a9e3D9Fd9022013eE0A419493e) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Liquidation.sol) |
| Exec | 0x59828FdF7ee634AaaD3f58B19fDBa3b03E2D9d80 | [Etherscan](https://etherscan.io/address/0x59828FdF7ee634AaaD3f58B19fDBa3b03E2D9d80) | [Etherscan](https://etherscan.io/address/0x14cBaC4eC5673DEFD3968693ebA994F07F8436D2) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Exec.sol) |
| Swap | 0x7123C8cBBD76c5C7fCC9f7150f23179bec0bA341 | [Etherscan](https://etherscan.io/address/0x7123C8cBBD76c5C7fCC9f7150f23179bec0bA341) | [Etherscan](https://etherscan.io/address/0xe20582e7FB2E5D1D96D8c8A65B4cdC3F5Dc398f8) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Swap.sol) |
| Governance | 0xAF68CFba29D0e15490236A5631cA9497e035CD39 | [Etherscan](https://etherscan.io/address/0xAF68CFba29D0e15490236A5631cA9497e035CD39) | [Etherscan](https://etherscan.io/address/0x554ee3d9ed7E9ec21E186c7dd636430669812f73) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) |


### Ropsten

| Contract | Proxy Address | Etherscan (Proxy) | Etherscan (Implementation) | Source Code |
|-------|------|------|------|------|
| Euler | 0xfC3DD73e918b931be7DEfd0cc616508391bcc001 | | [Etherscan](https://ropsten.etherscan.io/address/0xfC3DD73e918b931be7DEfd0cc616508391bcc001) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/Euler.sol) |
| Markets | 0x60Ec84902908f5c8420331300055A63E6284F522 | [Etherscan](https://ropsten.etherscan.io/address/0x60Ec84902908f5c8420331300055A63E6284F522) | [Etherscan](https://ropsten.etherscan.io/address/0x0131DD364E9cAeCf3426DcaD4bf2681b3816444B) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Markets.sol) |
| Liquidation | 0xf9773f2D869Bdbe0B6aC6D6fD7df82b82C998DC7 | [Etherscan](https://ropsten.etherscan.io/address/0xf9773f2D869Bdbe0B6aC6D6fD7df82b82C998DC7) | [Etherscan](https://ropsten.etherscan.io/address/0xe6b5Cc3Da62fF1422143843d4ff3Ad1c94328c50) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Liquidation.sol) |
| Exec | 0xF7B8611008Ed073Ef348FE130671688BBb20409d | [Etherscan](https://ropsten.etherscan.io/address/0xF7B8611008Ed073Ef348FE130671688BBb20409d) | [Etherscan](https://ropsten.etherscan.io/address/0x8bE3F14630D395F6Bfa8886261F6E13DaD775f64) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Exec.sol) |
| Swap | 0x86ea9f57d81Bf0C69Ff71114522fB3f29230DbA6 | [Etherscan](https://ropsten.etherscan.io/address/0x86ea9f57d81Bf0C69Ff71114522fB3f29230DbA6) | [Etherscan](https://ropsten.etherscan.io/address/0xf8a4bbbE6Cf87F2a142E20500B0D208Da7dF3204) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Swap.sol) |
| Governance | 0x78eE171d6c8d3808B72dAb8CE647719dB3bb4cC9 | [Etherscan](https://etherscan.io/address/0x78eE171d6c8d3808B72dAb8CE647719dB3bb4cC9) | [Etherscan](https://ropsten.etherscan.io/address/0x45B49e1cF05899D369cC3043eD0143Edf24b061a) | [GitHub](https://github.com/euler-xyz/euler-contracts/blob/master/contracts/modules/Governance.sol) |



_Note: the Governance smart contract is currently used for our risk-guarded launch (Phase 1 of the mainnet launch) while we build up to community-led governance in Phase 2._
