# Leverage

## Interface

* `getSupportedChainIds()`: Returns the supported chain IDs.
* `getSupportedMarketIds()`: Returns the supported market IDs for the respective chain.
* `leverage.getTokens()`: Returns the tokens available for use in the market.
* `leverage.getQuote()`: Returns the **position changes** to display, **approval/permit** to sign, and **leverage positions logics**.
* `buildTransactionRequest()`: Returns transaction data for leveraged operations.

## Logics behind

1. Initiates a flash loan the leverage token.
2. Deposit the leverage token to the user.
3. Borrow the base token from the market.
4. Swap the base token to the leverage token.
5. Repay the flash loan with a fee.
6. Deposit the remaining tokens, if any.

