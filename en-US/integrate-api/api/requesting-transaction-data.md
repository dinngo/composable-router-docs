# Requesting Transaction Data

### Build Router Transaction Request Data API

{% swagger method="post" path="/transactions" baseUrl="/v1" summary="Get transaction data of logics combinations" %}
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

{

&#x20;   \[

&#x20;       id: String,

&#x20;       rid: String,

&#x20;       fields: Logic Quote

&#x20;   ]

}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="slippage" type="Number" %}
The maximum allowed slippage for  logic if needed.

Default basis point is 100 (1%)

Example: swap-token logic
{% endswagger-parameter %}

{% swagger-parameter in="body" name="permitData" type="Object" %}
The PermitData for permit2
{% endswagger-parameter %}

{% swagger-parameter in="body" name="permitSig" type="String" %}
The user's signature in permitData
{% endswagger-parameter %}

{% swagger-parameter in="body" name="referralCode" type="Number" %}
A string containing tracking information about the referrer of the integrator.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
{% code lineNumbers="true" %}
```javascript
{
  "to": "0x67e4d4Af097787Aa5a7daE7f9b147Bf32243F030",
  "data": "0x1c81999100000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000032000000000000000000000000000000000000000000000000000000000000004c00000000000000000000000000000000000000000000000000000000000000780000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba300000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000028000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001842b67b570000000000000000000000000aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000ffffffffffffffffffffffffffffffffffffffff00000000000000000000000000000000000000000000000000000000645faecd00000000000000000000000000000000000000000000000000000000000000000000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000643828d500000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000041bb8d0cf3e494c2ed4dc1057ee31c90cab5387b8a606019cc32a6d12f714303df183b1b0cd7a1114bd952a4c533ac18606056dda61f922e030967df0836cf76f91c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba300000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000180000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008436c78516000000000000000000000000aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa0000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b208000000000000000000000000000000000000000000000000000000003b9aca00000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e592427a0aece92de3edee1f18e0157c0586156400000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000002400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000144c04b8d59000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000643828d6000000000000000000000000000000000000000000000000000000003b9aca0000000000000000000000000000000000000000000000000000000000003612330000000000000000000000000000000000000000000000000000000000000042a0b86991c6218b36c1d19d4a2e9eb0ce3606eb480001f4c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20001f42260fac5e5542a773aa44fbcfedf7c193bc2c599000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000000000000000000000000000000000000000000000000000000003b9aca0000000000000000000000000087870bca3f3fd6335c3f4ce8392d69350b4fa4e200000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000001800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000084617ba0370000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c5990000000000000000000000000000000000000000000000000000000000369e050000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c599ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff0000000000000000000000000000000000000000000000000000000000369e0500000000000000000000000000000000000000000000000000000000000000030000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c5990000000000000000000000005ee5bf7ae06d1be5997a1a72006fe6c607ec6de8000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
  "value": "0"
}
```
{% endcode %}
{% endswagger-response %}
{% endswagger %}

This endpoint provides the transaction request to be sent, which will essentially include the Router contract `address` (to), transaction `data` (data), and ETH to be carried in the transaction (value).

<pre class="language-javascript"><code class="lang-javascript">const getRouterTransactionRequest = async (chainId, account, logics) =>, {
    const result = await client.post('/v1/transactions', {
        body: {
            chainId: chainId,
            account: account,
            logics: logics,
        }
<strong>    });
</strong>    return result.data;
}

const chainId = 1;
const account = USER_ADDRESS;
const logics = [swapLogic, supplyLogic];

const transactionRequest = await getEstimateResult(chainId, account, logics);
</code></pre>

The result contains a list of chains that looks the following:

```json
{
  "to": "0x67e4d4Af097787Aa5a7daE7f9b147Bf32243F030",
  "data": "0x1c81999100000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000032000000000000000000000000000000000000000000000000000000000000004c00000000000000000000000000000000000000000000000000000000000000780000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba300000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000028000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001842b67b570000000000000000000000000aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000ffffffffffffffffffffffffffffffffffffffff00000000000000000000000000000000000000000000000000000000645faecd00000000000000000000000000000000000000000000000000000000000000000000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000643828d500000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000041bb8d0cf3e494c2ed4dc1057ee31c90cab5387b8a606019cc32a6d12f714303df183b1b0cd7a1114bd952a4c533ac18606056dda61f922e030967df0836cf76f91c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba300000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000180000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008436c78516000000000000000000000000aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa0000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b208000000000000000000000000000000000000000000000000000000003b9aca00000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e592427a0aece92de3edee1f18e0157c0586156400000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000002400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000144c04b8d59000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000643828d6000000000000000000000000000000000000000000000000000000003b9aca0000000000000000000000000000000000000000000000000000000000003612330000000000000000000000000000000000000000000000000000000000000042a0b86991c6218b36c1d19d4a2e9eb0ce3606eb480001f4c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20001f42260fac5e5542a773aa44fbcfedf7c193bc2c599000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000000000000000000000000000000000000000000000000000000003b9aca0000000000000000000000000087870bca3f3fd6335c3f4ce8392d69350b4fa4e200000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000001800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000084617ba0370000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c5990000000000000000000000000000000000000000000000000000000000369e050000000000000000000000009e2a2394c69874545c013492d52d1dc0c607b20800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c599ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff0000000000000000000000000000000000000000000000000000000000369e0500000000000000000000000000000000000000000000000000000000000000030000000000000000000000002260fac5e5542a773aa44fbcfedf7c193bc2c5990000000000000000000000005ee5bf7ae06d1be5997a1a72006fe6c607ec6de8000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
  "value": "0"
}
```
