# Oracle Rating

## **What is an oracle?**

Within the context of pricing, an oracle is an on-chain API for price. Differently put, it simply tells you what the price of an asset is at a given time.&#x20;

## Oracle Risk

While we think Uniswap's oracles are best suited for our permissionless lending protocol, depositing into an Euler pool backed by illiquid liquidity pools on Uniswap can lead to devastating results.&#x20;

If the Uniswap V3 oracle of the borrowed asset is manipulated to the upside, the attack could trigger liquidations and sweep borrowers' collateral.&#x20;

Even more of concern is when the attacker can manipulate the asset pricing to the downside. Hypothetically, if the price drops to almost zero, the attacker only needs a small amount of collateral to borrow the entire pool and run away with a hefty profit.&#x20;

## Euler’s Oracle Risk Grading System

There are two main factors that influence the ease of attacking a Uniswap V3 oracle: TVL and concentration of liquidity.&#x20;

This is why we’ve come up with a rating that incorporates 3 factors:

### TVL locked in the Uniswap V3 pool:

![](https://cdn-images-1.medium.com/max/1000/1\*M2xlub1qmc-hqY7ly-jHcw.png)

### Slippage on a $1mil XYZ vs ETH buy order on Uniswap:

![](https://cdn-images-1.medium.com/max/1000/1\*hF4E9s0dgqGvTkdBjH-NSQ.png)

### Slippage on a $1mil XYZ vs ETH sell order on Uniswap:

![](https://cdn-images-1.medium.com/max/1000/1\*Leu9q4CQu03CHBy5UD\_lgw.png)

### The sum of these ratings yields a comprehensive rating:

![](https://cdn-images-1.medium.com/max/1000/1\*ELg4AQ5eo\_5uSotJgjSsJw.png)

Which will be displayed on the front-end page of the respective lending pool:

![](https://cdn-images-1.medium.com/max/1000/1\*Y0tqJ3WmEcg3mMJjBAzB8A.jpeg)

The overall rating goes from A to F (A meaning good and F meaning avoid at all cost) and should give users an idea of what the oracle risk is. _**Overall, anything below B should probably be avoided!**_

**Keep in mind that this is merely an indicative tool and we bear no responsibility for loss of funds.**
