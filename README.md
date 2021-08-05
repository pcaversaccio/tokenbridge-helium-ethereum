# Tokenbridge Helium to Ethereum
A **Tokenbridge** between the [Helium blockchain](https://www.helium.com) - commonly referred to as the *native* network - and the [Ethereum blockchain](https://ethereum.org) - commonly referred to as the *foreign* network.

## 1. Blockchain Bridges - Background
A cornerstone technology of blockchain interoperability is the **blockchain bridge**. Blockchain bridges are ways for two economically sovereign and technologically diverse chains to communicate with each other. Blockchain bridges come in a variety of forms, from centralised and trusted to more decentralised and trustless. We definitely prefer the latter forms of bridges for our ecosystem, but there is nothing to stop a development team from building and deploying the former.

### 1.1 Bridging Methods
> Most of the information in this section is based on inputs from [Polkadot's wiki](https://wiki.polkadot.network/docs/learn-bridges). We strongly recommend anyone who wants to dive deeper to read the wiki carefully.

Building a bridge that is as decentralised and trustless as possible can be done through any of the following methods (ordered by suggested methodology):
- *Bridge pallets* - For Substrate-native chains, use a bridge pallet (e.g. Kusama `\<\>` Polkadot bridge, since both networks' parachains use Substrate).
    > Very simply put, [Substrate](https://www.substrate.io) is a software library that can help any developer build his/her own custom blockchain. Substrate is created by [Parity Technologies](https://www.parity.io) and provides the basis for [Polkadot](https://polkadot.network). For any further details, we recommend reading the article: [Substrate in a nutshell](https://www.parity.io/blog/substrate-in-a-nutshell).

- *Smart contracts* - If the chain is not on Substrate, we should have smart contracts on the non-Substrate chain to bridge (e.g. the Ethereum mainnet will have a bridge smart contract that initiates ether (ETH) transactions based on incoming [XCMP](https://wiki.polkadot.network/docs/learn-crosschain) messages).
- *Higher-order protocols* - If the chain does not support smart contracts (e.g. Bitcoin), we should use [XCLAIM](https://www.xclaim.io) or similar protocols to bridge.

### 1.2 Examples
#### Ethereum Bridge (Smart Contracts `\<\>` Polkadot)
As explained by Dr. Gavin Wood in a high-level [blog post](https://medium.com/polkadot-network/polkadot-substrate-and-ethereum-f0bf1ccbfd13) from October 2019, there are three ways that e.g. the Polkadot and Substrate ecosystem can be bridged to the Ethereum ecosystem:
1. Polkadot <-> Ethereum public bridge;
2. Substrate <-> Parity-Ethereum-PoA bridge;
3. The Substrate EVM module;

#### Bitcoin Bridge (XCLAIM `\<\>` Substrate `\<\>` Polkadot)
The [Interlay](https://interlay.io) team has written a [specification](https://interlay.gitlab.io/interbtc-spec) on a Bitcoin bridge that is based on the [XCLAIM](https://eprint.iacr.org/2018/643.pdf) design paper. The protocol enables a two-way bridge between Polkadot and Bitcoin. It allows holders of BTC to *teleport* their assets to Polkadot as *PolkaBTC*, and holders of *PolkaBTC* to burn their assets for BTC on the Bitcoin chain.

The Bitcoin bridge as documented in the specification is composed of two logically different components:
- The [XCLAIM component](https://github.com/interlay/interbtc-spec/tree/master/interbtc-spec) that maintains all accounts that own PolkaBTC;
- The [BTC-Relay](https://github.com/interlay/interbtc-spec/tree/master/btcrelay-spec) that is responsible for verifying Bitcoin state when a new transaction is submitted.

There is now a [reference implementation and testnet available](https://bridge.interlay.io/?tab=issue).

## 2. Bridging Helium to Ethereum - Proposed Path
Helium in its current state, as well as Ethereum, is not a Substrate-native chain, so we cannot use *bridge palettes*. Furthermore, the Helium blockchain does not support any smart contract functionality nor is it based on the Ethereum Virtual Machine (EVM). Also, unfortunately, a Turing-complete smart contract functionality is not part of the [Helium Improvement Proposals](https://github.com/helium/HIP). Whilst the implementation of such a feature is challenging, we strongly recommend submitting a proposal for this functionality as it will be an important feature for the management of IoT devices (e.g. part ownership, partial payments). Remember, a normal multi-signature wallet is already smart contract. Due to these facts, we cannot use approaches like [TokenBridge](https://docs.tokenbridge.net) that allow users to transfer data (e.g. digital asset ownership information) between two chains in the Ethereum ecosystem. Generally, EVM-based cross-chain bridges provide fast and secure connections between blockchains and create scalability and connectivity - interoperability - between Ethereum networks.

Therefore, we are left with deploying a higher-order protocol to implement a decentralised bridge system. Since Interlay has successfully showcased the [XCLAIM](https://www.xclaim.io) protocol for the Bitcoin `\<\>` Polkadot bridge, we recommend building the Helium `\<\>` Ethereum on the same foundation.

## 3. License
The [`tokenbridge-helium-ethereum`](https://github.com/pcaversaccio/tokenbridge-helium-ethereum) implementation is licensed under the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html), also included in our repository in the [`LICENSE`](https://github.com/pcaversaccio/tokenbridge-helium-ethereum/blob/main/LICENSE) file.

## 4. References
[1] https://wiki.polkadot.network/docs/learn-bridges

[2] https://github.com/interlay/interbtc-spec

[3] https://docs.interlay.io
