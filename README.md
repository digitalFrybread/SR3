<div align="center">

  <h1><code>SR3</code></h1>

  <strong>A template for kick starting a Rust and Blockchain project using <a href="https://github.com/paritytech/substrate">Substrate</a>.</strong>

  <h3>
    <a href="https://substrate.io/">Docs</a>
    <span> | </span>
    <a href="https://matrix.to/#/!HzySYSaIhtyWrwiwEV:matrix.org?via=matrix.parity.io&via=matrix.org&via=web3.foundation">Chat</a>
  </h3>

</div>

## Features

This template includes the minimum required components to start a PoS testnet, inspired by [substrate-node-template](https://github.com/substrate-developer-hub/substrate-node-template).

* Consensus related pallets: Babe & GRANDPA
* Staking related pallets: staking, session, authorship, im-online, offences, utility
* Governance related pallets: collective, membership, elections-phragmen, democracy, treasure

**Notes:** The code is un-audited and not production ready, use it at your own risk.

## Getting Started

Follow the steps below to get started.

### Rust Setup

First, complete the [Dev Docs Installation](https://docs.substrate.io/v3/getting-started/installation/).

### Build and Run

Use the following command to build the node and run it after build successfully:

```sh
cargo build --release
./target/release/SR3 --dev
```

## Run public testnet

* Modify the genesis config in chain_spec.rs
* Build spec, `./target/release/SR3 build-spec --chain staging > SR3-staging.json`
* Change original spec to encoded raw spec, `./target/release/SR3 build-spec --chain=SR3-staging.json --raw > SR3-staging-raw.json`
* Start your bootnodes, node key can be generate with command `./target/release/SR3 key generate-node-key`.
  ```shell
  ./target/release/SR3 \
       --node-key <your-node-key> \
       --base-path /tmp/bootnode1 \
       --chain SR3-staging-raw.json \
       --name bootnode1
  ```
* Start your initial validators,
  ```shell
  ./target/release/SR3 \
      --base-path  /tmp/validator1 \
      --chain   SR3-staging-raw.json \
      --bootnodes  /ip4/<your-bootnode-ip>/tcp/30333/p2p/<your-bootnode-peerid> \
	    --port 30336 \
	    --ws-port 9947 \
	    --rpc-port 9936 \
      --name  validator1 \
      --validator
  ```
* [Insert session keys](https://substrate.dev/docs/en/tutorials/start-a-private-network/customchain#add-keys-to-keystore)
* Attract enough validators from community in waiting
* Call force_new_era in staking pallet with sudo, rotate to PoS validators
* Enable governance, and remove sudo
* Enable transfer and other functions
