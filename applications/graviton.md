# Open Grant Proposal

> This document is referenced in the terms and conditions and therefore needs to contain all the required information. Don't remove any of the mandatory parts presented in bold letters or as headlines! See the [Open Grants Program Process](https://github.com/w3f/Open-Grants-Program/blob/master/README_2.md) on how to submit a proposal.

* **Project:** Graviton
* **Proposer:** DeFi-Evangelist
* **Payment Address:** 1BeRKVozn3X7wiByvYBryPWugFvvrp61ug

## Project Overview :page_facing_up: 

### Overview
* A brief description of the project: 
  
[Graviton](https://graviton.one/), a logical continuation of the [Gravity protovol](https://gravity.tech), provides financial incentives and a governance framework for providers of cross-chain transfers and AMM liquidity for wrapped tokens. 

Graviton infrastructure is represented by three products:

- Cross-chain token gateway service ([SuSy Gateway](https://medium.com/gravity-protocol/susy-a-blockchain-agnostic-cross-chain-asset-transfer-gateway-protocol-based-on-gravity-9d5b1550e5f4))
- Single-sided liquidity service for wrapped tokens
- Liquidity incentivisation network & governance portal

We are the founders and core developers of the tokenless oracle protocol [Gravity](https://arxiv.org/pdf/2007.00966.pdf), which aims to be a blockchain-agnostic solution. [Graviton](https://graviton.one/) is an application on top of Gravity network designed to improve the user experience with wrapped tokens and gateways, and to incetivize gateway oracles and AMM liquidity providers in various target chains.


### Reason for the application
Polka tech (Substrate / Polkadot / Kusama) is going to be integrated into the Gravity network as a target-chain (and a deposit-chain). We believe that there will be more DeFi services on Polka/Kusama chains in upcoming months/years, and we'd like to contribute to this ecosystem.

Within the scope of this grant application, we plan to develop two core components for Graviton:

_**- polka/kusama cross-chain transfer gateway infrastructure and service**_

(chains: polka/kusama <-> tron, binance smart chain (bsc), waves)

_**- on-chain single-sided liquidity service for wrapped tokens**_

P.S.: At this moment, it is difficult to propose a comprehensive technical explanation of how exactly the integration and ssAMM service will look like. In addition, the functionality of parachains in Polka or Kusama networks is limited to fulfill our use case at the moment, so we are expecting some trade-offs between temporary intermediate solutions and the final properly designed solution.


### Project Details 
We are planning to start off by creating a Parity Substrate-based Gravity chain (gravity-substrate-chain) with pBFT consensus, where validators are represented by Gravity consuls ([most reputable nodes](https://arxiv.org/pdf/2007.00966.pdf)). The SYSTEM-SC and NEBULA-SC will be deployed on the gravity-substrate-chain, as well as a SuSy gateway (via Gravity, the decentralized oracle).

This temporary solution will serve as an infrastructure for building the gateway and the single-sided liquidity AMM service for wrapped tokens.
It will be maintained up to the moment when Kusama/Polka chains begin to fully support parachains in mainnets.

When possible, we are going to make a hardfork of gravity-substrate-chain to modify the consensus and the list of validators, turning it into a parachain of Kusama/Polka networks ("gravity-substrate-chain -> gravity-parachain" (GSC -> GPC) migration).

Before the mainnet launch, we will perform and test this migration in testnet.

#### Mockups:
Draft UI mockups for crosshcain swap service - [SuSy Gateway UI](https://www.figma.com/file/y67ljpuoDzt2Zv6NJRTeTm/Rabbit_Ex_figma?node-id=0%3A1).

#### Working demo:
Testnet demo for Waves->Ethereum chains - [crosschain swap demo service](https://susy.gravity.tech/swap)

#### Tech stack:
Go, Rust, Solidity, Parity Substrate, Type Script, Vue.js, polkadot{.js}, Docker

### Details about Protocols

* GSC - gravity-substrate-chain (v0)
* GPC - gravity-parachain (v1)

- To create token transfer gateways, we are planning to implement [SuSy](https://arxiv.org/abs/2008.13515) protocol between GSC/GPC chain and Binance Smart Chain (BSC) (or/and any other chain integrated into the Gravity network: Tron, Ethereum, Waves):

![SuSy LU->IB flow](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/susy-flow.png)

- Core on-chain/off-chain functionality of the gateway will be managed via [Gravity protocol](https://arxiv.org/pdf/2007.00966.pdf):

![Gravity-Flow](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/gravity-flow.png)

- Gravity is a decentralized oracle represented by Gravity nodes/oracles which participate in a consensus process called Pulse. 
Pulse consensus is composed of two steps of data verification.

I. (off-chain) Commit-Reveal step:

![Gravity-Pulse CR step](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/gravity-pulse-cr.png)
 
II. (on-chain) Augmented Threshold Signature step:

![Gravity-Pulse AV step](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/gravity-pulse-av.png)

- SuSy crosschain gateway is an implementation of USER-SC contracts on both chains as LU (lock/unlock) or IB (issue/burn) "ports". Its security is ensured by a dynamically assembled subset of Gravity oracles:

![Gravity-SC](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/gravity-smartcontracts.png)

- To bring liquidity and a better UX for users of wrapped tokens on destination chains, it is necessary to build/support/incentivise AMM services on destination chains (especially single-sided liquidity AMM LPs):

![Graviton Liquidity Mining Flow](https://raw.githubusercontent.com/ventuary-lab/images/master/graviton/graviton-lm.png)


#### Research papers:
- [Gravity Protocol](https://arxiv.org/abs/2009.05540)
- [SuSy Protocol](https://arxiv.org/abs/2008.13515)
- [Graviton Liquidity Network](https://arxiv.org/abs/2007.00966)

### Ecosystem Fit 
There are several projects in the Polka ecosystem similar to Graviton:

"Bifrost - A parachain designed for staking liquidity (Wave 5)" and "Substrate/Ethereum Bridge - ChainSafe and Centrifuge were awarded a grant in W3F Grants"
 
Similarities:
- token bridge based on multiple signings

Differences:
- EOS-Polka bridge or ETH-Polka bridges atm. Gravity will bring all integrated chains simultaneously after GSC/GPC implementation.
(chains: polka/kusama <-> tron, binance smart chain (bsc), waves)
- No service infrastructure on target-chains (nebula-sc or user-sc lego flexible structure).
- Gravity validators and signers are managed by p2p reputation scores.
- Graviton is also a single-sided AMM service within a target-chain.

Graviton is not yet another gateway for Polkadot/Kusama nets. Graviton infrastructure is represented by three products:
- Cross-chain token gateway service ([SuSy Gateway](https://medium.com/gravity-protocol/susy-a-blockchain-agnostic-cross-chain-asset-transfer-gateway-protocol-based-on-gravity-9d5b1550e5f4)).
- Single sided liquidity service for wrapped tokens.
- Liquidity incentivisation network & governance portal.


## Team :busts_in_silhouette:

### Team members

Team Lead / Tech Lead:
Aleksei Pupyshev - [twitter](https://twitter.com/AlekseiPupyshev), [linkedin](https://www.linkedin.com/in/aleksei-pupyshev-23a70954/)

Team members:
Ilya Sapranidi (researcher), Shamil Khalilov (front-end), Ilya Teterin (blockchain), Regina Chernyavska (design)

### Team Website	
Team:
* https://venlab.dev/

Tech/Dev:
* https://gravity.tech/

* https://graviton.one/

### Legal Structure 
Aleksei Pupyshev - individual entrepreneur license (Russia)

### Team's experience
The Graviton project is being built by VenLab blockchain research & development team, founded by Aleksei Pupyshev in 2018. VenLab’s track record:

* “Mastering Web 3.0” online course for developers on [Stepik](https://stepik.org/course/54415/promo) and [Coursera](https://www.coursera.org/learn/mastering-web3-waves?#instructors)

~3k learners, ~1k developers in [dev chat](https://t.me/waves_ride_dapps_dev)

* [Neutrino](https://neutrino.at/) [($USDN)](https://coinmarketcap.com/currencies/neutrino-usd/) - An algorithmic crypto-collateralized stablecoin (acquired by [WX](https://waves.exchange/))

~50mln$ Total Value Locked (TVL), ~7k dApp users, ~30mln$ market cap & ~3mln$ volume

* [Gravity Protocol](https://medium.com/gravity-protocol) - A blockchain-agnostic oracles and cross-chain communication network

5 integrated chains so far, 21+ reputable node operators


### Team Code Repos
* https://github.com/ventuary-lab
* https://github.com/Gravity-Tech

### Team LinkedIn Profiles
* https://www.linkedin.com/in/aleksei-pupyshev-23a70954/

## Development Roadmap :nut_and_bolt: 

### Overview
* **Total Estimated Duration:** 3 months
* **Full-time equivalent (FTE):** 3.5
* **Total Costs:** 1.8 BTC

### Milestone 1 — Gravity-Parachain
* **Estimated Duration:** 1 month
* **FTE:**  1.2
* **Costs:** 0.6 BTC

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 1. | Parity Substrate | Parity Substrate with dynamic set of validators from consuls (top-k most reputapable nodes) of gravity network |  
| 2. | Parachain Integration | Connection of chain based on substrate to polkadot/kusama network |  
| 3. | SuSy Gateway Integration Tests |  Crosschain gateway functionality within integration tests based on separate independent docker containers |


### Milestone 2 — Crosschain Swap Demo
* **Estimated Duration:** 1 month
* **FTE:**  1.1
* **Costs:** 0.6 BTC

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 1. | polkadot{.js} | Integration with polkadot{.js} |  
| 2. | Deployment into testnets | Transition of the gateway functionality from integration tests into the stable network |  
| 3. | Demo UI | Basic UI for manual testings of crosschain swaps |  


### Milestone 3 — Full-Functioning Crosschain Swaps & Single Sided AMM Liquidity Pool for wrapped tokens
* **Estimated Duration:** 1 month
* **FTE:**  1.2
* **Costs:** 0.6 BTC

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 1. | Full-Functioning Crosschain Swaps UI/UX | Production ready functionality of crosschain transfers between parahcain and gravity chains (eth, bsc, tron, waves)|  
| 2. | Single Sided AMM Liquidity Pool | Uniswap-Like pools without slippage with price based on data feed from oracles |
| 3. | Liquidity Mining | Liquidity Mining functionality for liquidity and transfer providers (gateway oracles) |

## Future Plans

A) multichain network of liquidity for wrapped tokens

B) interchain governance system for graviton network


