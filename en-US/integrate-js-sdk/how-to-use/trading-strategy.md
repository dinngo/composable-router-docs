# 1⃣ Trading Strategy

Before using the SDK, it's important to have a clear understanding of your trading **strategy**. This will help you make informed decisions when using the SDK to send transaction. Below, we provide an example scenario to help illustrate how to define a trading strategy. You can use this as a guide to customize your own strategy.

#### **Example**

Suppose a user has 1000 USDC in Ethereum and wants to swap it for WBTC to supply the WBTC pool on the Aave V3 lending platform and earn interest.

The user's address is `0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa`.

Typically, the user needs to perform two actions:&#x20;

1. Exchange **USDC** to **WBTC** by **Uniswap V3**&#x20;
2. Supply **WBTC** to get **aWBTC** by **Aave V3**

Each of the actions mentioned above represents a `Logic` in the Composable Router. The following sections will guide you on how to build these logics and send the transaction successfully.
