# UI

## How to connect to metamask

* Click the Connect button at the top right of the page.
* Select metamask from the list.
* Enter your password into the metamask popup to unlock your metamask.
* Ensure you have selected the correct wallet; and your network is set to the correct one.


## How to send a transaction

### Approve, Deposit, Withdraw, Borrow, Repay
* Make sure your wallet is connected; and you have funds in your wallet for the corresponding asset in question.
* Go to the individual market page you are interested in.
* If you have not already, you will need to Approve transactions against this asset.

#### Deposit
Enter the amount you wish to deposit (or hit Max*) and this will add it to our batch transaction slip.

#### Withdraw
Enter the amount you wish to withdraw (or hit Max*) and this will add it to our batch transaction slip.

#### Borrow
Enter the amount you wish to borrow (or hit SafeMax*) and this will add it to our batch transaction slip.

#### Repay
Enter the amount you wish to repay (or hit Max*) and this will add it to our batch transaction slip.

* Under the hood Max sends MaxUint256 to the server, which tells the contract to send everything (even dust that is accumulated during the time taken for the block to get mined)) <- CHECK
* SafeMax finds the maximum amount you can borrow without bringing your health score below 1.25, this is based on the collateral you have deposited.
* Max withdraw looks at how much is available to withdraw from the bucket and how much you wish to withdraw and sets the maximum possible available amount.

### Transfer ETokens, Transfer DTokens, Toggle Collateral
* Make sure your wallet is connected.
* Go to the Dashboard page from the top navigation.

#### Transfer ETokens
* Click the Transfer ETokens button to induce the modal popup
* fill out the form: where the tokens are coming from, going to and what asset you are interested in.
* Note that this only sends ETokens, not real tokens.
* Additionally, be aware that your accounts are protocol specific, do not attempt to write out your subaccount address, please use the subaccount id from the dropdown. <- CHECK
* Click submit to add the transaction to the batch transaction slip

### Transfer DTokens
* Click the Transfer DTokens button to induce the modal popup
* fill out the form: where the tokens are coming from, going to and what asset you are interested in.
* Note that this only sends DTokens, not real tokens, and sending DTokens is effectively sending debt to that account.
* Additionally, be aware that your accounts are protocol specific, we try to make the underlying subaccounts addresses to protect our users, do not attempt to write out your subaccount address, please use the subaccount id from the dropdown. <- CHECK
* Click submit to add the transaction to the batch transaction slip

### Toggle Collateral
* Ensure that you have no outstanding borrows on the account.
* Click the toggle collateral button to add a collateral toggle to the transaction slip.

### Transaction slip
* This can be expanded out from the right side of the UI at any point.
* Everytime you alter your transaction slip it automatically checks how much gas you will spend and tries to figure out if there are any going to be any errors.
* Transactions are executed in the order you have specified and the order of the transactions can be re-arranged in a drag and drop fashion.
* You are able to send transactions from different accounts (more on that later) at the same time.


### Accounts
* Part of opening up ourselves to lending on every market means that we have to protect the system against volatile and potentially malicious tokens. To do this we have categorised assets as isolated, cross and collateral. <- Check
* If the asset is isolated then you are only able to borrow and lend on one single asset per sub account.
* To create a new account is free and simple, you just have to press the plus button in the top right navigation and you will automatically add a new subaccount and simulateonously switch to it.

