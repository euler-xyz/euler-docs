---
description: >-
  Learn about different errors users might encounter from time on the UI and
  what they mean
---

# Common Errors

### You have a collateral violation

Collateral violation means you're trying to borrow something without having enough collateral in your account to do so. Make sure you deposit a collateral asset first, like USDC. You can filter collateral assets on the markets page.

### No match, code: NETWORK\_ERROR

Please try refreshing the page and make sure you have a stable internet connection and your web3 wallet is on the correct RPC network (e.g., Goerli Test Network).

### No match, code: UNPREDICTABLE\_GAS\_LIMIT

Try refreshing the page and trying the transaction again. This error also often occurs for other reasons. So if you keep having this issue, please check your browser’s console log and please report the error that it shows.

### Unknown error

Please try refreshing the page. If you receive the same error message, please check your browser’s log for errors and create a support ticket with what you find.

### Transfer amount exceeds balance, please check you have enough tokens in your wallet and make sure they are also not deposited into Euler

You don't have enough tokens in your wallet. If using the test, please make sure you have the correct testnet tokens from the official Euler testnet faucet.

### execution reverted: e/too-many-entered-markets

For a given account, you can enter 10 markets max. You should try the transaction with another account or sub-account.

### RPC error

Some RPC providers on the market (i.e. [Flashbots Protect RPC](https://docs.flashbots.net/flashbots-protect/rpc/quick-start/)) are not compatibile with Euler simulation mode. If this error occurs, the user is advised to change the RPC (i.e. by changing the network in Metamask to default Ethereum network) and refresh the dapp. Having done that, the simulation feature should be functional again.

If, due to any reason, user wants to use their originally selected RPC to send the transaction, the following should be done (example described based on Metamask, actions might differ for other wallets):
- change the RPC to default Ethereum network
- add all the desired transactions to the batch
- assure that the simulation is passing without any error
- click 'Send txs' button
- when Metamask pops up 
   - click on 'New address detected! Click here...' at the top. Then click 'Add a nickname'. Input 'Euler Exec' as a nickname and click 'Save'
   - click on 'HEX', scroll down and click 'Copy raw transaction data'
   - click 'Reject'
   - disregard the error in the dapp
   - open Metamask and click 'Send'
   - select previously added 'Euler Exec' address
   - leave the asset set to ETH
   - leave the amount as 0 ETH
   - paste your clipboard contents into the 'Hex Data' field
   - change the network to desired
   - click 'Next' and sign the transaction
