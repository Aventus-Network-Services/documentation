# ERC-20 Token Lift

This guide takes a user through the steps required to submit a lift transaction for ERC-20 tokens from Ethereum mainnet to the Aventus Network via the contract interface on Etherscan.

Prerequisites:
- You'll need custody of the full amount of tokens you want to lift in one of your Ethereum accounts
- Web3 available in your browser
- and a small amount of ETH to send the transactions

## Approval

Before the lift can be submitted you first need to approve the amount to be transferred.

1. Go to the ERC-20 token contract of the token you want to lift on Etherscan, click on the 'Contract' tab, and then 'Write Contract'.

> example ERC-20 token = `0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb`
>
> example Etherscan page = `https://etherscan.io/address/0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb#writeContract`

2. Connect to Web3 with Metamask (or similar) on the account that will be approving the tokens.

3. Expand the '2. approve' method and enter the required parameters in the `(address)` and `(uint256)` fields.

> In the `(address)` field enter the address of the AvnFTScalingManager Contract (`0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68`) for approval
>
> In the `(uint256)` field enter the amount of the token you wish to lift in full Wei value (Typically tokens use 18 decimal places, this conversion can be easily got from: https://eth-converter.com/) example: `1VOW` = `1000000000000000000`

> Example snippet:
> ```
> (address) = 0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68
> (uint256) = 1000000000000000000
> ```

4. Click the 'Write' button to begin the process. This will trigger Metamask and ask for you to 'Approve' your transaction. Now wait for the transaction Status to show 'Success'.

## Lift

Now the tokens have been approved we need to visit the AvnFTScalingManager contract to start the lift.

1. Go to the [AvnFTScalingManager Contract](https://etherscan.io/address/0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68#writeContract)

2. Connect to Web3 with Metamask on the same account again

3. Expand the '2. lift' method and enter required parameters in the `(address)`, `(bytes32)` and `(uint256)` fields.

> In the `(address)` field enter the address of the ERC-20 Token Contract you're lifting (`0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb`)
>
> In the `(bytes32)` field enter the public address in the Aventus Network that you'd like to lift the tokens to (if you're lifting for yourself ensure you know the private key to be able to access these tokens once lifted!). For example: `0x96072be954594e63b21737b492031c965b363e6c575016e6249b1aa64e8f1170`
>
> In the `(uint256)` field enter the amount of the token you wish to lift in Wei as before

> Example snippet:
> ```
> _erc20Contract (address) = 0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb
> _t2PublicKey (bytes32) = 0x96072be954594e63b21737b492031c965b363e6c575016e6249b1aa64e8f1170
> _amount (uint256) = 1000000000000000000
> ```

4. Click the 'Write' button to begin the process. This will trigger Metamask and ask for you to 'Approve' your transaction. Now wait for the transaction Status to show 'Success' and save the Transaction Hash
