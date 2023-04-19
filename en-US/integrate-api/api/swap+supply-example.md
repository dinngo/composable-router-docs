# Swap+Supply (Example)

The following section will explain step by step how to swap token by Uniswap and supply token to Aave protocol.

### Step 1: Prepare strategy used token

Users have 1000 USDC, which needs to be exchanged for WBTC and supply to Aave Protocol to earn interest. This scenario will require two logic

1. Exchange **USDC** to **WBTC** by **Uniswap V3**&#x20;
2. Supply WBTC to get **aWBTC** by **Aave V3**

Obtain the required Token information according to the Request Tokens API

```javascript
const client = axios.create({ baseURL: 'https://ethtaipei-router-api.furucombo.app' });
const getSwapTokens = async () => {
    const result = await client.get('/v1/protocols/1/uniswap-v3/swap-token/tokens');
    return result.data;
}
```

### Step 2: Build the Logics

The request for first logic quote is exchange 1000 USDC to WBTC by Uniswap V3 looks the following:

```javascript
const getSwapQuote = async (inputToken, inputAmount, tokenOut) => {
    const result = await client.get('/v1/protocols/1/uniswap-v3/swap-token/quote', {
        params: {
            input: {
                token: inputToken,
                amount: inputAmount
            },
            tokenOut: tokenOut,
        }
    });
    return result.data;
}

const inputToken = USDC;
const inputAmount = '1000';
const tokenOut = WBTC;

const swapQuote = await getSwapQuote(inputToken, inputAmount, tokenOut);
const swapLogic = {
    id: uuidv4(),
    rid: 'uniswap-v3:swap-token',
    fields: swapQuote,
}
```

Than second logic is use above swap output token (WBTC) and amount supply to Aave V3 and get aWBTC looks the following:

```javascript
const getSupplyQuote = async (inputToken, inputAmount, tokenOut) => {
    const result = await client.post('/v1/protocols/1/aave-v3/supply/quote', {
        body: {
            input: {
                token: inputToken,
                amount: inputAmount
            },
            tokenOut: tokenOut,
        }
    });
    return result.data;
}

const inputToken = swapQuote.output.token;
const inputAmount = swapQuote.output.amount;
const tokenOut = aWBTC;

const supplyQuote = await getSupplyQuote(inputToken, inputAmount, tokenOut);
const supplyLogic = {
    id: uuidv4(),
    rid: 'aave-v3:supply',
    fields: supplyQuote,
}
```

### Step 3: Estimate Router Data

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

It is suggested that a permit can be used so that users do not have to send multiple transactions and have a better experience in the future.

### Step 4: Build Router Transaction

After the demand for the estimate of logics is confirmed, the user of this case permits USDC for the first time.&#x20;

```javascript
const signer = provider.getSigner(account);
const permitData = estimateResult.permitData;
const permitSig = await signer._signTypedData(permitData.domain, permitData.types, permitData.values);
```

You can then use the request router transaction data method to get the transaction request.

```javascript
const getRouterTransactionRequest = async (chainId, account, logics, slippage) => {
    const result = await client.post('/v1/transactions', {
        body: {
            chainId: chainId,
            account: account,
            logics: logics,
            slippage: slippage,
            permitData: permitData,
            permitSig: permitSig,    
        }
    });
    return result.data;
}

const chainId = 1;
const account = USER_ADDRESS;
const logics = [swapLogic, supplyLogic];
const slippage = 300; // 3%

const transactionRequest = await getEstimateResult(chainId, account, logics, slippage);
```

### Step 5: Sending the Transaction

This is the Router transaction to be sent next. If you're using `ethers` package, you can refer to the code example to send the transaction:

```javascript
const signer = provider.getSigner(account);
const tx = await signer.sendTransaction(transactionRequest);
```

We hope this example helps you get started quickly. If you have any questions or suggestions, please feel free to create an issue on Github, and we will respond as soon as possible.

