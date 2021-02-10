# ERC-20 Token Lift

This guide takes a user through the steps required to submit a lift transaction for ERC-20 tokens from Ethereum to the Aventus Network via the contract interface on Etherscan.

## Approval

You'll need custody of the full amount of tokens you want to lift in one of your Ethereum accounts and Web3 available in your browser. Before the lift can be submitted you first need to approve the amount to be transferred.

1. Go to the ERC-20 token contract of the token you want to lift on Etherscan, click on the 'Contract' tab, and then 'Write Contract'.

> example ERC-20 token = `0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb`
>
> example Etherscan page = `https://etherscan.io/address/0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb#writeContract`

2. Connect to Web3 with Metamask (or similar) on the account that will be approving the tokens.

3. Expand the '2. approve' method and enter the required parameters in the `(address)` and `(uint256)` fields.

> Enter the address of the AvN Contract for contract approval in the `(address)` field
>
> Enter the amount `(uint256)` of the token you wish to lift in full Wei value (Easily get the full token value in Wei from: https://eth-converter.com/)
> example: `1VOW` = `1000000000000000000`

> ```
> guy (address) = 0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68
> wad (uint256) = 1000000000000000000
> ```

4. Click the 'Write' button to begin the process. This will trigger Metamask and ask for you to 'Approve' your transaction. Now wait for the transaction Status to show Success.

## Lift

1. Go to [0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68](https://etherscan.io/address/0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68#writeContract)

2. Connect to Web3 with Metamask on the same account again

3. Expand the '2. lift' method and enter: 

> ```
> _erc20Contract (address) = 0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb
> _t2PublicKey (bytes32) = 0x96072be954594e63b21737b492031c965b363e6c575016e6249b1aa64e8f1170
> _amount (uint256) = 1000000000000000000
> ```

4. Click the 'Write' button to begin the process. aThis will trigger Metamask and ask for you to 'Approve' your transaction. Now wait for the transaction Status to show Success and save the Transaction Hash