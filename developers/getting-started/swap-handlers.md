# Swap Handlers

Swap handlers are contracts, external to the Euler platform, which are used by the `SwapHub` module to execute trades through a common API.
The user can select any swap handler when calling a function of the `SwapHub`. The `SwapParams` struct passed to the handler defines a type of trade (exact input vs exact output), requested token amounts and slippage settings. Additional `payload` bytes array can be used to encode off-chain any additional data required by the handler. From the perspective of the `SwapHub` module, the handler is a black box. `SwapHub` transfers tokens required for the trade to the handler before invoking the `executeSwap` function the handlers are expected to expose. `SwapHub` only requires that the resulting balances after calling the handler fall within the user requested bounds.

Currently, 3 swap handlers are available in the Euler repo:
* Uniswap V3 handler, which executes swaps by calling the functions of the UniswapV3 periphery [SwapRouter](https://github.com/Uniswap/v3-periphery/blob/main/contracts/SwapRouter.sol)
* Uniswap [smart order router](https://github.com/Uniswap/smart-order-router) handler, which executes off-chain encoded split trades on Uniswap V2 and V3
* 1Inch handler, which executes trades quoted by [1Inch Aggregation Protocol API](https://docs.1inch.io/docs/aggregation-protocol/api/swagger)

## Combined Handlers
Exact output swaps are most useful when repaying a debt through `SwapHub`'s `swapAndRepay` function. If the user want's to repay the full debt, the exact amount
that needs to be received from the trade is only known during the transaction execution, since debt interest accrues every second. Any off-chain calculated
amount will be outdated by the time the transaction is mined. For that reason, for exact output swaps, the Uniswap Smart Order Router handler and 1Inch handlers, 
perform a primary swap defined by the off-chain payload and additionally trade for the remainder (presumably accrued interest) through a secondary swap, directly 
on UniswapV2 or V3. They are therefore referenced to as **combined** handlers.

## Security Considerations for Swap Handler Developers
Swap handlers are not expected to hold any token balances. They receive input tokens from `SwapHub` and are expected to perform the trade by any means necessary, and return both the output as well as any left-over input. There is a possibility however that the handler might hold some token balances - either because of user mistake or an attempt of a griefing attack. If the handler doesn't account for it, i.e. it simply transfers all balances back unconditionally, it might return an unexpected amount of either input or output token. The consequesces from `SwapHub`'s perspective are different for exact input and exact output swaps:

1. Exact input, handler holds output token balance.

Any additional output returned to SwapHub is credited to the user.

2. Exact input, handler holds input token balance.

`SwapHub` accepts returns of unused input token and credits them to the user, unless the returned amount is higher than what was provided to the handler, in which case it reverts. If the handler holds enough balance, such that after executing the swap, the balance is still larger than what was provided by the `SwapHub`, the transaction would fail.

3. Exact output, handler holds output token balance.

During a regular swap, extra amount will be credited to the user, `swapAndRepay` however will revert with 'repay too much' error.

4. Exact output, handler holds input token balance.

Similar to scenario 2, the only difference being that the amount of input provided by `SwapHub` is the maximum allowed amount consumed by exact output swap.

In scenarios 2. and 4. there is a possibility of a griefing attack by transferring tokens to the handler. It would be costly however, since the attacker needs to send more input tokens than the swap he wants to disrupt, and the next swap of a bigger size will simply consume his deposit, as a bonus to the user. Euler swap
handlers ignore this possibility.

Scenario 3. however is different in case of `swapAndRepay`. Even a very small amount of extra output token, a single wei in fact, will revert the transaction. For this reason, current swap handlers don't return the output token to `SwapHub`. Instead, they expect the call to the DEX to designate the Euler contract to be the receiver of the output.

In case of combined swap handlers, a problem of extra output token in `swapAndRepay` could also occur if the primary swap returns more tokens than expected. The payload for the primary swap is encoded off-chain. Before the transaction is mined, the slippage could cause the trade to yield more than the debt and the transaction would revert. This scenario is accepted, and should be accounted for by the UI. If the transaction fails despite that, it might be actually in the user's favor, because it might mean the market moves in favor of the swapper.