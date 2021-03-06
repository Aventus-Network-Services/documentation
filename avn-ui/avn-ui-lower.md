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

# Proxy Lower Page

## Summary

Lowering of ERC20/ERC77 tokens from AVN network to Ethereum is a cross-chain operation which requires transactions on both tiers. A relayer who has a proof from an AVN user(aka. lowerer) account and would like to pay the transaction fee in AVT on Tier2 for the lowerer can dispatch a signed_lower extrinsic within a proxy call. The complete cross-chain process can be break down into the following steps:

1. Verify the proxy T2 lower transaction and record it in a summary and checkpointed on T1
  a. An AVN user signs a signature for a lower extrinsic to allow a relayer lower tokens from a lowerer T2 account.
  b. The relayer dispatches a proxy call on AVN with a signed lower extrinsic by lowerer in the call data, and signs the proxy extrinsic to pay the transaction fee from relayer’s AVT account.
  c. The signed lower extrinsic is then created on T2 and voted to be included in a summary, which would be published on T1 later.

2. Get lower data from AVN service through rpc call. Send a `lower_data` rpc call to an avn-node to get the lower transaction leaf and its merkle path.
3. The user calls the lower transaction on T1 to claim the lowered tokens from T1 treasury account.

Signed Lower page from the avn-ui collects all the information required for this complete proxy lower process and the following fields must be specified:

Tier 1 Contract addresses
- AvN Tier 1 Lower contract address: The Ethereum address of the AvnFTScalingManager contract
- AvN Tier 1 treasury contract address: The Ethereum address of the AvnFTTreasury contract
- Token address: The Ethereum address of the tokens being lowered

Tier 1 User credentials
- Web3 provider url: The ethereum network provider, localhost for local deployment or a link to the testnet through infura.
- Ethereum address of transaction sender to Ethereum: The Ethereum address of an account who holds some ETH to pay the gas when claiming the lowered tokens on tier1.
- Private key of the ethereum sender: The private key of the sender. We can use the MetaMask connected account by disabling the `Use private key`.

RPC node
- Rpc node url: A url that is used to get lower_data from AVN network.

Lower data
- Relayer: The account who will pay AVT and send the signed lower transaction in tier2. This account could be the same as the Lowerer account described below.
- Lowerer: This account is the owner of the tokens being destroyed in tier2.
- Amount to lower: The amount of tokens to lower (in attoAVT - 18 decimal places)
- Tier1 recipient address: The Ethereum address of the account that can claim those tokens on tier1. This account must be the sender of the Tier1 lower transaction.
- Lowerer proof: A signature, signed by the lowerer, authorising the relayer to send a signed lower transaction on their behalf for the specified amount. This field is automatically populated, or can be generated by clicking the “Generate signature” button.

Informational only fields:
- AVN20 Balance of lowerer on Tier 2: Lowerer's token balance on tier2
- AVN20 Balance of recipient on Tier 1: Lowerer's token balance on tier1
- Total tokens locked on Tier 1: Amount of token on tier 1 that can be lowered

## Tracking progress

The Signed lower progress field will display the logs generated by the signed-lower page.

## Generating lowerer proofs

If lowerers want to generate a lower proof, but not send the transaction to the AvN on tier2, they can fill in the correct data and click on Generate lowerer signature only. This will create a proof (signature) that can be copied.
