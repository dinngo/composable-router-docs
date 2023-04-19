# Estimate Logics Result

### Estimate Logics Transaction API

{% swagger method="post" path="/transactions?isEstimate=true" baseUrl="/v1" summary="Get information about estimating logic combinations" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="chainId" type="Number" required="true" %}
The chain id.

Example: 1, 137
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="String" required="true" %}
The user address.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="logics" type="Array" required="true" %}
The logics data.

\[

&#x20;   {

&#x20;       id: String,

&#x20;       rid: String,

&#x20;       fields: Logic quote,

&#x20;   },

&#x20;   ....

]
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% code lineNumbers="true" %}
```javascript
{
  "funds": [
    {
      "token": {
        "chainId": 1,
        "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
        "decimals": 6,
        "symbol": "USDC",
        "name": "USD Coin"
      },
      "amount": "1000"
    }
  ],
  "balances": [
    {
      "token": {
        "chainId": 1,
        "address": "0x5Ee5bf7ae06D1Be5997A1A72006FE6C607eC6DE8",
        "decimals": 8,
        "symbol": "aEthWBTC",
        "name": "Aave Ethereum WBTC"
      },
      "amount": "0.03579397"
    }
  ],
  "approvals": [
    {
      "to": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
      "data": "0x095ea7b3000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba3ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
    }
  ],
  "permitData": {
    "domain": {
      "name": "Permit2",
      "chainId": 1,
      "verifyingContract": "0x000000000022D473030F116dDEE9F6B43aC78BA3"
    },
    "types": {
      "PermitSingle": [
        { "name": "details", "type": "PermitDetails" },
        { "name": "spender", "type": "address" },
        { "name": "sigDeadline", "type": "uint256" }
      ],
      "PermitDetails": [
        { "name": "token", "type": "address" },
        { "name": "amount", "type": "uint160" },
        { "name": "expiration", "type": "uint48" },
        { "name": "nonce", "type": "uint48" }
      ]
    },
    "values": {
      "details": {
        "token": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
        "amount": "0xffffffffffffffffffffffffffffffffffffffff",
        "expiration": 1683882982,
        "nonce": 0
      },
      "spender": "0x9E2A2394C69874545C013492d52d1DC0c607b208",
      "sigDeadline": 1681292782
    }
  }
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

This endpoint provides an estimate of how much funds will be spent (**funds**) and how many balances will be obtained (**balances**) from this transaction. It will also identify any approvals that the user needs to execute (**approvals**) before the transaction and whether there is any permit2 data that the user needs to sign before proceeding (**permitData**).

```javascript
const getEstimateResult = async (chainId, account, logics) => {
    const result = await client.post('/v1/transactions?isEstimate=true', {
        body: {
            chainId: chainId,
            account: account,
            logics: logics,
        }
    });
    return result.data;
}

const chainId = 1;
const account = USER_ADDRESS;
const logics = [swapLogic, supplyLogic];

const estimateResult = await getEstimateResult(chainId, account, logics);
```

The result contains a list of chains that looks the following:

```json
{
  "funds": [
    {
      "token": {
        "chainId": 1,
        "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
        "decimals": 6,
        "symbol": "USDC",
        "name": "USD Coin"
      },
      "amount": "1000"
    },
    ... // all other tokens will be spent
  ],
  "balances": [
    {
      "token": {
        "chainId": 1,
        "address": "0x5Ee5bf7ae06D1Be5997A1A72006FE6C607eC6DE8",
        "decimals": 8,
        "symbol": "aEthWBTC",
        "name": "Aave Ethereum WBTC"
      },
      "amount": "0.03579397"
    },
    ... // all other tokens will be obtained
  ],
  "approvals": [
    {
      "to": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
      "data": "0x095ea7b3000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba3ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
    },
    ... // all other needs to execute (approvals) before the transaction
  ],
  "permitData": {
    "domain": {
      "name": "Permit2",
      "chainId": 1,
      "verifyingContract": "0x000000000022D473030F116dDEE9F6B43aC78BA3"
    },
    "types": {
      "PermitSingle": [
        {
          "name": "details",
          "type": "PermitDetails"
        },
        {
          "name": "spender",
          "type": "address"
        },
        {
          "name": "sigDeadline",
          "type": "uint256"
        }
      ],
      "PermitDetails": [
        {
          "name": "token",
          "type": "address"
        },
        {
          "name": "amount",
          "type": "uint160"
        },
        {
          "name": "expiration",
          "type": "uint48"
        },
        {
          "name": "nonce",
          "type": "uint48"
        }
      ]
    },
    "values": {
      "details": {
        "token": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
        "amount": "0xffffffffffffffffffffffffffffffffffffffff",
        "expiration": 1683990224,
        "nonce": 0
      },
      "spender": "0x9E2A2394C69874545C013492d52d1DC0c607b208",
      "sigDeadline": 1681400024
    }
  }
}
```

### Funds (Initial Funds)

This is the number of initial funds needed in the logic combination, e.g. the subsequent logic is the token generated by the previous logic, so the user does not have to transfer it again, so it is not counted.

### Balances (You will receive)

This is an estimate of the amount of money that will be returned to your wallet at the end of the transaction and is easily displayed to the user.

### Approvals

After the current estimation, there are still transactions that require user authorization, such as the first time a user uses permit2 or borrow delegation.

### PermitData

The first time the permit2 token is used for Composable Router, the user's signature is required. The default validity period of the signature is `30 minutes`, and the expiration time of the Token permit is `30 days`.

