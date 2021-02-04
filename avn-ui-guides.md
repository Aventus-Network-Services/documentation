# Accounts Page

## Summary

This page shows a summary of all accounts that can be used to interact with the AvN. These accounts can be added and stored locally or injected via a browser extension.

From this page a user can:
  - Check the crypto used to create the account
  - Any tags associated with an account. These are user defined "flags"
  - The number of transactions submitted from an account
  - The AVT balance

Users can also:
  - send AVT
  - send tokens
  - Lift tokens and
  - Lower tokens

## Adding accounts

To add a local account:
  - Click on `Add account` located on the top right corner of the page
  - Specify the name of the account
  - Choose the secret (private key) generation method: Mnemonic or Raw seed and specify it
  - Set a password for the account

Advanced users can also specify the cryto used to generate an account and any derivation paths. This advanced feature can be found by expanding the `Advanced creation options` section, located at the bottom of the modal.

Once all the relevant information has been added, clicking next will show a summary of the data and an option to either cancel the operation, go back or save the account. Clickin on save will create the account and download an account recovery file that should be kept safe.

## Recovering accounts

To recover an account, user can use the `Restore JSON` functionality by clicking on the `Restore JSON` button located at the top righ corner of the page.

From this page you can upload the recovery file and specify the password used when the account was created to restore it.

# Lift Page

## Summary

This page allows users to lift tokens from tier1 to tier2. Lift is a cross chain operation and requires interacting with Ethereum and AvN so the page is split into 2 sections

## Tier1 - Ethereum

In order to lift tokens, users have to lock their tokens in a special smart contract (AvN contract). The AvN contract supports 2 types of tokens ERC20 and ERC777. The current implementation only support ERC20 tokens, which requires 2 tier1 transactions to lock:
  - Approve the transfer of tokens from the ERC20 contract to the AvN contract
  - Lock the approved tokens in the AvN contract.

### Specifying a Tier1 transaction sender (msg.sender)

This page allows you to specify who the sender should be when sending transactions on tier1. There are 2 different ways this can be accomplished:
  - Using Metamask or
  - Using address and private key

#### Using Metamask - default setting

Metamask is the default setup, and when a user lands on this page Metamask will automatically pop-up and ask permission to be linked to this page. If Metamask is not installed the page will show an error in the console.

If Metamask is installed and logged in, the user will be prompted to choose an account to interact with this page. If its not logged in, the user will be asked to log in.

Once logged in and linked to an account, the `User ethereum address` field will be populated with the address of the selected user and the `User token balance` will also be updated to show the tier1 token balance of the user.

The `Contract token balance` shows the amount of tokens locked up in the AvN contract on tier1 and the `AvN tier1 contract address`, as the name suggests, shows the address of the AvN contract on Rinkeby.

#### Using address and private key

To use this setting:
  - Click on the `use private key` toggle button
  - Specify the user address in `User ethereum address` and
  - Specify the corresponding private key in `Private key for user address`

The `User token balance` will automatically update when a valid address is specified.

### Lifting on tier1 (Ethereum)

Once a user is selected, the second step is to send the transactions to lift. For this a user has to specify:
  - The tier2 recipient of the lifted tokens (`Tier2 recipient public key`): This must be a hex encoded 32 byte public key. ex: `0x322060a8ef38d23ecef28cc34b8e98d1013b471e4efac121218e21cbd3a9d109`
  - The token address that is being lifted (`token to lift`): The ethereum address of the ERC20 token. ex: `0x82Fea31F3f2bF9E555c9A27Aa4CfAF3ec2468C1e`
  - The amount of tokens lifted (`Amount to lift`): The number of tokens to lift in wei (18 decimal places). ex: `1000000000000000000`

## Lifting on Tier2

When the tokens are locked up on tier1, the smart contract emits an event signalling the successful tier1 lift and any user with AVT can send a transaction to the AvN and lift those tokens to tier2. To send this transaction we need:
  - A tier2 user with AVT (`Lift transaction sender`): The user who will pay AVT to send the lift transaction
  - The ethereum transaction hash that corresponds to the lift (`Ethereum transaction hash`): This fiel is read-only by default and will be automatically populated when tier1 processes the lift.

## Resuming a lift

To just send an AvN transaction for an existing tier1 lift, a user can:
  - Click on the `AvN lift only` toggle button
  - Specify a sender (`Lift transaction sender`)
  - Specify a valid ethereum transaction hash (`Ethereum transaction hash`) and click on `Lock tokens on Ethereum and lift to Tier2` button

## Tracking progress

The `Lift progress` field will display the logs generated by the lift page. When a lift transaction has been added to the AvN on tier2, the `Pending events` field will be populated with details of the lift transaction including the block number it will be executed on. This field will be cleared automatically when the lift is executed.

# Transfer Page

## Summary

This page allows users to transfer any lifted tokens on tier2.

## Transfering tokens

To transfer tokens, the following fields must be specified:
  - `Relayer`: The account who will pay AVT and send the signed transfer transaction to the AvN. This account can be the same as the `From` account described below.
  - `Relayer public key`: Auto populated field that shows the public key of the selected relayer
  - `Sender public key`: The public key of the account who is sending the tokens
  - `Receiver public key`: The public key of the account who is receiving the tokens
  - `Token`: The Ethereum address of the token being transfered
  - `Amount to transfer`: The amount of tokens being transfered, in wei (18 decimal places)
  - `Sender proof`: A signature, signed by the sender, authorising the relayer to send a `transfer` transaction on their behalf for the specified amount. This field is automatically populated

There are also 2 information only fields:
  - `Sender token balance`: Sender's token balance on tier2
  - `Receiver token balance`: Receiver's token balance on tier2

## Generating transfer proofs

If users want to generate a transfer proof, but not send the transaction to the AvN on tier2, they can fill in the correct data and click on `Generate transfer signature only`. This will create a proof (signature) that can be copied.

## Unlocking accounts

Before an account is able to sign, it needs to be unlocked. The first time users get to this page, they would be prompted to unlock the selected `Sender public key` accouont. Clicking on `Unlock account` will bring up a modal where users can type the password and click on `unlock`.

## Tracking progress

The `Transfer progress` field will display the logs generated by the transfer page.

# Lower Page

## Summary

This page allows users to transfer any lifted tokens on tier2. Lowering is a cross chain operation and requires transactions on both tiers.

## Lowering on Tier2

Lowering on tier2 is a transaction that will destroy token from tier2 in order to reclaim them on tier1. To lower on tier2, users need to specify the following:
  - `Sender`: The account that will pay AVT and send the lower transaction on tier2. This account must also be the owner of the tokens being destroyed.
  - `Token`: The Ethereum address of the tokens being lowered
  - `Amount to lower`: The amount of tokens to lower (in wei - 18 decimal places)
  - `Tier1 recipient address`: The Ethereum address of the account that can claim those tokens on tier1. This account must be the sender of the Tier1 lower transaction.
  - `Lower account`: Read-only field automatically populated with a special address that point to a lower account.

## Tier1 - Ethereum

### Specifying a Tier1 transaction sender (msg.sender)

This page allows you to specify who the sender should be when sending transactions on tier1. There are 2 different ways this can be accomplished:
  - Using Metamask or
  - Using address and private key

#### Using Metamask - default setting

Metamask is the default setup, and when a user lands on this page Metamask will automatically pop-up and ask permission to be linked to this page. If Metamask is not installed the page will show an error in the console.

If Metamask is installed and logged in, the user will be prompted to choose an account to interact with this page. If its not logged in, the user will be asked to log in.

Once logged in and linked to an account, the `User ethereum address` field will be populated with the address of the selected user and the `User token balance` will also be updated to show the tier1 token balance of the user.

The `Contract token balance` shows the amount of tokens locked up in the AvN contract on tier1 and the `AvN tier1 contract address`, as the name suggests, shows the address of the AvN contract on Rinkeby.

#### Using address and private key

To use this setting:
  - Click on the `use private key` toggle button
  - Specify the user address in `User ethereum address` and
  - Specify the corresponding private key in `Private key for user address`

The `User token balance` will automatically update when a valid address is specified.

### Lowering on Tier1 (Ethereum)

In order to lower on tier1 the following pre-requisits must be met:
  - Tokens have to be lowered on tier2
  - The lower transaction has to be included in a summary generated on tier2. This summary will include all paying transactions for a given block range.
  - The summary has to be published on Tier1 by calling the `PublishRoot` method of the AvN contract.

Once the above mentioned pre-requisits have been met, users can send a `lower` transaction to tier1 and unlock the tokens. To send a lower transaction users must specify:
  - The ABI encoded leaf: Leaf data that represent a single lower transaction on Tier2. This leaf has an encoded field that Ethereum can decode and understand.
  - Merkle path: The path from this lead to a merkle root that has been previously registerd as part of a `PublishRoot` method call. This will act as proof that the leaf was contained in the merkle tree whose root we have registered previously.

These values can be obtained by calling a public rpc endpoing on any AvN node that allows rpc connections. The `RPC node URL` field should be used to specify the full URL, including port numbers.

## Tracking progress

The `Lower progress` field will display the logs generated by the lower page.
