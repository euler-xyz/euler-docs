<a id="definitions"></a>
## Definitions

 * Liquidity pool:
 * Permissionless lending: 
 * Perpetual loan: loan take over a period of several blocks, but without a specified repayment date.
 * Flash loan: loan taken from a liquidity pool that is repayable within the same atomic transaction.
 * Time-weighted average price (TWAP): the average price of an asset calculated over some historical interval of time.  
 * Collateral factor: parameter that governs what percentage of the market value of an asset can be used as collateral for borrowing.
 * Borrow factor: parameter that governs by what percentage a user must over-collateralise in order to borrow an asset. 
 * Over-collateralised: state in which a user has provisioned more collateral value than their liability value.
 * Under-collateralised: state in which a user has not provisioned enough collateral value to cover their liabilities. 
 * Insolvency: a state in which the market value of a user's collateral is worth less than the market value of their liabilities, meaning they no longer have an incentive to repay their loan.
 * Health score: The ratio of a user's collateral value to the value of their liabilities. When above 1, it means they are over-collateralised. When below 1, it means they are under-collateralised.
 * Collateral value: The value of a user's collateral that can be used to borrow other assets. It is calculated as the market value of a user's collateral multiplied by the relevant collateral factors. 
 * Liability value: The value of a user's borrows after adjusting to make sure they are over-collateralised. It is calculated as the market value of a user's borrows divided by the relevant collateral factors. 
 * Liquidationn event in which a user's collateral assets are exchanged for the assets they borrowed in order to bring them back to an over-collateralised state.     
 * Static interest rate: a type of model used on Compound and Aave in which the interest rate is constrained to be a function of the utilisation rate of a liquidity pool.
 * Reactive interest rate: a new type of interest rate model backed by control theory that allows interest rates to react freely to market conditions.  
 * Compound interest: the result of perpetually earning interest on interest already accrued.  
 * Euler XYZ: the initial developers of Euler Protocol.
 * Euler DAO: the decentralised autonomous organisation that will manage Euler Protocol and the Euler Treasury.
 * Euler Protocol: the collection of smart contracts comprising the protocol.
 * Euler Governance Token (EUL)] EUL tokens represent voting shares in Euler governance. A holder can vote on each proposal themselves or delegate their votes to a third party.