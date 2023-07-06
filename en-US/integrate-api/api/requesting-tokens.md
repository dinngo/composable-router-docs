# Requesting Tokens

### Get Logic Tokens API

{% swagger method="get" path="/{chainId}/{protocol}/{logicId}/tokens" baseUrl="/v1/protocols" summary="List of tokens of protocol logic that are available" %}
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

{% swagger-response status="200: OK" description="" %}
{% code lineNumbers="true" %}
```javascript
{
   "tokens":[
      {
         "chainId":1,
         "address":"0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
         "decimals":6,
         "symbol":"USDC",
         "name":"USD Coin"
      },
      ...
   ]
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

This endpoint provides a list of tokens supported by Logic, depending on the chain and protocol.

```javascript
const client = axios.create({ baseURL: 'https://api.protocolink.com' });
const getTokens = async (chainId, protocol, logicId) => {
    const result = await client.get(`/v1/protocols/${chainId}/${protocol}/${logicId}/tokens`);
    return result.data;
}

const chainId = 1;
const protocol = "uniswap-v3";
const logicId = "swap-token";

const tokens = await getTokens(chainId, protocol, logicId);
```

The result contains a list of chains that looks the following:

```json
{
   "tokens":[
      {
         "chainId":1,
         "address":"0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
         "decimals":6,
         "symbol":"USDC",
         "name":"USD Coin"
      },
      ... // other tokens will be present in the list
   ]
}
```

Presented according to different protocols or the token has been paired:

```json
：{
   "tokens":[
      [
         {
            "chainId":1,
            "address":"0x0000000000000000000000000000000000000000",
            "decimals":18,
            "symbol":"ETH",
            "name":"Ethereum"
         },
         {
            "chainId":1,
            "address":"0x4d5F47FA6A74757f35C14fD3a6Ef8E3C9BC514E8",
            "decimals":18,
            "symbol":"aEthWETH",
            "name":"Aave Ethereum WETH"
         }
      ],
      ... // other token pair will be present in the list
   ]
}j
```
