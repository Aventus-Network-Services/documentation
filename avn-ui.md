# AvN UI

The core functionality of the Aventus Network can be accessed via graphical user interface forked from Polkadot referred to as the AvN UI. This can be run locally or accessed via a hosted cloud version and simply needs to connect to the network via a URL.

There are multiple instances of the Aventus Network running (prod, testnet, QA, etc.) so the UI can be used to interface any of these networks.

repo - https://github.com/ArtosSystems/avn-ui

## Setup

NOTE: The testnet will have been configured with a set of data as defined by the latest zip file in this directory - eg avn_testnet_v.0.0.6.zip - use that for any settings, accounts, etc referred to here

### Using polkadotJS

1. Open polkadotjs on your browser by navigating to: https://polkadot.js.org/apps/#/explorer
2. Click on the Settings button from the left hand menu (if its not selected by default) 
3. Under the Developer tab copy and paste the contents (including the curly brackets) of the [custom types file](https://github.com/ArtosSystems/avn-tier2/blob/master/custom_types.json)
4. Under the General tab enable custom endpoint and type the following url: wss://eu-west-1.avntestnet.artos.io
5. Click on the Save & Reload button
6. The page should reload and you should see the full list of menu items to interact with the network. You are now connected to the boot node, which is also a validator.

### Running Locally

To start off, this repo (along with others in the @polkadot family) uses yarn workspaces to organize the code. As such, after cloning dependencies should be installed via `yarn`, not via `npm`, the latter will result in broken dependencies.

1. Clone the repo locally, via `git clone https://github.com/ArtosSystems/avn-ui`
2. Ensure that you have a recent LTS version of Node.js, for development purposes Node >=10.13.0 is recommended.
3. Ensure that you have a recent version of Yarn, for development purposes Yarn >=1.10.1 is required.
4. Install the dependencies by running `yarn`
5. Ready! Now you can launch the UI (assuming you have a local Polkadot Node running), via `yarn run start`
6. Access the UI via http://localhost:3000

### Hosted AvN UI

Or alternatively connect to a remote node running in AWS here http://ec2-34-224-213-239.compute-1.amazonaws.com:3000/#/avnAccounts

1. Click on the Settings button from the left hand menu (if its not selected by default) 
2. Under the Developer tab copy and paste the contents (including the curly brackets) of the [custom types file](https://github.com/ArtosSystems/avn-tier2/blob/master/custom_types.json)
3. Under the General tab enable custom endpoint and type the following url: wss://eu-west-1.avntestnet.artos.io
4. Click on the Save & Reload button
5. The page should reload and you should see the full list of menu items to interact with the network. You are now connected to the boot node, which is also a validator.

#### Pre-funded accounts

By default none of the built-in accounts will have any AVT so if you want to send transactions via polkadotjs you need to add an account with some AVT.
There are 2 validators with 1000 AVT each and you can add them by following these steps:

1. Click on the Accounts button from the left hand menu
2. Click on the Add account button located at the top of the page
3. Give it any name you want
4. Use the mnemonic from one of the account JSON files in the 10-nodes/keys directory of the latest config zip
5. Type in a password
6. Leave the key pair type on Schnorrkel
7. Leave the secret derivation path empty
8. Save and download recovery file

You can repeat these steps to add both Validator accounts if required

#### Joining the network

To join the network as a listener node (Synch node) you can connect to the boot node using: 
`--bootnodes /dns/ec2-54-171-210-24.eu-west-1.compute.amazonaws.com/tcp/30333/p2p/12D3KooWSu5C6EvRgY7AaDsnn9WW372go9P2k7Gs63P7rQFwZi5X`

The chainspec file required to join the network (validatorSpecRaw.json) is stored in the same folder as this document.

An example command to run a node to join the test network:

`./target/release/avn-node --base-path /node/myNodeData --chain /avn.testnetSpecRaw.json --name myNode --port 30334 --ws-port 9945 --rpc-port 9934 --bootnodes /dns/ec2-54-171-210-24.eu-west-1.compute.amazonaws.com/tcp/30333/p2p/12D3KooWSu5C6EvRgY7AaDsnn9WW372go9P2k7Gs63P7rQFwZi5X`

#### RPC calls

RPC calls to the boot node have to be done via HTTPS on port 9933. You can use curl or postman or any other client to make these calls. 

The full url is: https://eu-west-1.avntestnet.artos.io:9933

#### Tier1 contracts

AvN Tier 2 needs AvN Tier1 contracts to communicate with in order to process events.

See [here](https://github.com/ArtosSystems/avn-tier1/blob/master/migrationLog-rinkeby.txt) for the addresses of the latest contracts deployed on Rinkeby

Use https://rinkeby.etherscan.io/ to look at the transactions that have been sent to the contracts.

The main protocol contract should be verified, so you should be able to see the decoded event values in Etherscan by clicking on the:
Logs tab when viewing  a transaction (eg https://rinkeby.etherscan.io/tx/0xbac1ffaa4f35452fc647a1a7a73bca0023f323ba24b3eba2f0aa1291e51167a8#eventlog); or the
Events tab when viewing the contract (eg https://rinkeby.etherscan.io/address/0x19747d75c91ce389407b5d174ef96f87d897700e#events)
