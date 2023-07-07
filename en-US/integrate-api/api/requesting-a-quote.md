# Requesting a Quote

### Get Logic Quote API

{% swagger method="post" path="/{chainId}/{protocol}/{logicId}/quote" baseUrl="/v1/protocols" summary="The quote of logic" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="chainId" type="Number" required="true" %}
The chain id.

Example: 1, 137
{% endswagger-parameter %}

{% swagger-parameter in="path" name="protocol" required="true" type="String" %}
The protocol.

Example: uniswap-v3, aave-v3
{% endswagger-parameter %}

{% swagger-parameter in="path" name="logicId" required="true" type="String" %}
The logic Id.

Example: swap-token, supply
{% endswagger-parameter %}

{% swagger-parameter in="body" name="input" required="true" type="Object" %}
The token with amount

{

&#x20;   "token": {

&#x20;       "chainId": number,

&#x20;       "address": string,

&#x20;       "decimals": number,

&#x20;       "symbol": string,

&#x20;       "name": string

&#x20;   },

&#x20;   "amount": string

}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tokenOut" required="true" type="String" %}
The output token address\
{

&#x20;   "chainId": number,

&#x20;   "address": string,

&#x20;   "decimals": number,

&#x20;   "symbol": string,

&#x20;   "name": string

}
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% code lineNumbers="true" %}
```javascript
{
  "tradeType": "exactIn",
  "input": {
      "token": {
          "chainId": 1,
          "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
          "decimals": 6,
          "symbol": "USDC",
          "name": "USD Coin"
      },
      "amount": "1000"
  },
  "output": {
      "token": {
          "chainId": 1,
          "address": "0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599",
          "decimals": 8,
          "symbol": "WBTC",
          "name": "Wrapped BTC"
      },
      "amount": "0.03579397"
  },
  "path": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb480001f4c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20001f42260fac5e5542a773aa44fbcfedf7c193bc2c599"
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

This endpoint provides a quote of Logic, depending on the chain and protocol.

<pre class="language-javascript"><code class="lang-javascript"><strong>const getQuote = async (chainId, protocol, logicId, logicParams) => {
</strong>    const result = await client.post(`/v1/protocols/${chainId}/${protocol}/${logicId}/quote`, {
        body: logicParams,
    });
    return result.data;
}

const chainId = 1;
const protocol = "uniswap-v3";
const logicId = "swap-token";
const logicParams = {
    input: {
        token: USDC,
        amount: '1000'
    },
    tokenOut: WBTC,
    slippage: 100, // 1%
};

const swapQuote = await getQuote(chainId, protocol, logicId, logicParams);
</code></pre>

Quote is used in fields of Logic data. It can be used after building Logic according to the following format:

```javascript
const swapLogic = {
    rid: `${protocol}:${logicId}`,
    fields: swapQuote,
}
```

### Logic Params (default)

```javascript
// aave-v2: deposit, withdraw
// aave-v3: supply, withdraw
// uniswap-v3: swap-token (exact in)
// utility: wrapped-native-token
{
    input: {
        token: inputToken,
        amount: inputAmount
    },
    tokenOut: tokenOut,
    slippage: 100, // 1%
}

// uniswap-v3: swap-token (exact out)
{
    tokenIn: tokenIn,
    output: {
        token: inputToken,
        amount: inputAmount
    },
    slippage: 100, // 1%
}
```

The result contains a list of chains that looks the following:

```json
{
    "tradeType": "exactOut",
    "input": {
        "token": {
            "chainId": 1,
            "address": "0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599",
            "decimals": 8,
            "symbol": "WBTC",
            "name": "Wrapped BTC"
        },
        "amount": "0.03618858"
    },
    "output": {
        "token": {
            "chainId": 1,
            "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
            "decimals": 6,
            "symbol": "USDC",
            "name": "USD Coin"
        },
        "amount": "1000"
    },
    "path": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb480001f46b175474e89094c44da98b954eedeac495271d0f000bb82260fac5e5542a773aa44fbcfedf7c193bc2c599",
    "slippage": 100
}
```

### Compound Logics Params

```javascript
// compound-v3: supply-base, withdraw-base
{
    marketId: marketId
    input: {
        token: inputToken,
        amount: inputAmount
    },
    tokenOut: tokenOut,
}

// compound-v3: repay
{
    marketId: marketId
    borrower: USER_ADDRESS,
    tokenIn: tokenIn,
}

// compound-v3: claim
{
    marketId: marketId
    borrower: USER_ADDRESS,
    tokenIn: tokenIn,
}
```

The result contains a list of chains that looks the following:

```json
{
    "marketId": "USDC",
    "input": {
        "token": {
            "chainId": 1,
            "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
            "decimals": 6,
            "symbol": "USDC",
            "name": "USD Coin"
        },
        "amount": "1000"
    },
    "output": {
        "token": {
            "chainId": 1,
            "address": "0xc3d688B66703497DAA19211EEdff47f25384cdc3",
            "decimals": 6,
            "symbol": "cUSDCv3",
            "name": "Compound USDC"
        },
        "amount": "1000"
    }
}
```
