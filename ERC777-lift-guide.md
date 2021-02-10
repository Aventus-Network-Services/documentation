# ERC-777 Token Lift

This guide takes a user through the steps required to submit a lift transaction for ERC-20 tokens from Ethereum to the Aventus Network via the contract interface on Etherscan.

## Lift

1. Go to the ERC-777 token contract of the token you want to lift on Etherscan, click on the 'Contract' tab, and then 'Write Contract'.

> example ERC-20 token = `0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb`
>
> example Etherscan page = `https://etherscan.io/address/0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb#writeContract`

2. Connect to Web3 with Metamask (or similar) on the account that will be approving the tokens.

3. Expand the 'send' method and enter the required parameters in the `(address)`, `(uint256)` and `(bytes)` fields.

> For the `(address)` enter the address of the AvnFTScalingManager: `0x1Af691Cf6d6944C53e42dAAC8395e63F46186E68`
>
> Enter the amount of your token you wish to lift in `(uint256)` in full Wei value (Easily get the full token value in Wei from: https://eth-converter.com/) example: `1VOW` = `1000000000000000000`
>
> In the data `(bytes)` field enter an AvN Public Key, for example: `0xda6bd9d19caa75548eb0acde9eff9fdd94b2452ead5b0daf8f73364457641748`

> ```
> (address) = 0x1BBf25e71EC48B84d773809B4bA55B6F4bE946Fb
> (uint256) = 1000000000000000000
> (bytes) = 0xda6bd9d19caa75548eb0acde9eff9fdd94b2452ead5b0daf8f73364457641748
> ```

4. Click the 'Write' button to begin the process. This will trigger Metamask and ask for you to 'Approve' your transaction. Now wait for the transaction Status to show Success and save the Transaction Hash.
