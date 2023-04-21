# 3⃣ Estimate Router Data

To properly estimate the logics of the router results, closely follow the steps below.

### Step 1: Build Router Data

First, you need to prepare the Router Data, which will include the `chainId`, `account`, `logics`, and `slippage` data. By default, the slippage is optional and set to 1%. However, if you want to customize the slippage, you should specify it as a number, using Basis Points where 1 Basis Point equals 0.01%.

```typescript
import * as api from '@furucombo/composable-router-api';

const routerData: api.RouterData = {
  chainId,
  account: '0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa',
  logics: [swapLogic, supplyLogic],
  slippage: 300, // 3%
};
```

### Step 2: Estimate Router Data Result

Next, use `api.estimateRouterData` to estimate how much funds will be spent (funds) and how many balances will be obtained (balances) from this transaction. It will also identify any approvals that the user needs to execute (approvals) before the transaction and whether there is any permit2 data that the user needs to sign before proceeding (permitData).

```typescript
import * as api from '@furucombo/composable-router-api';

const estimateResult = await api.estimateRouterData(routerData);
```

The structure of the `estimateResult` obtained is roughly as follows:

```json
{
  "funds": [         // How much initial funds are needed
    {
      "token": ...,  // USDC
      "amount": "1000"
    }
  ],
  "balances": [      // How many tokens you will receive
    {
      "token": ...,  // aEthWBTC
      "amount": "0.03579397"
    }
  ],
  "approvals": [     // User approval before transaction if need
    {
      "to": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
      "data": "0x095ea7b3000000000000000000000000000000000022d473030f116ddee9f6b43ac78ba3ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
    }
  ],
  "permitData": {    // Token permit before transaction if need
    "domain": ...,
    "types": ...,
    "values": ...
  }
}

```

**Funds:** For this transaction, `1000 USDC` will be spent, which can be displayed on the interface.

**Balances:** For this transaction, `0.03579397 aEthWBTC` will be obtained, which can be displayed on the interface.

### Step 3: Approvals (optional)

For this transaction, the user needs to approve Permit2 contract to spend his USDC first. If using `ethers` package, you can refer to the following code snippet to help the user send approval transactions:

```typescript
const signer = provider.getSigner(account);
for (const approval of estimateResult.approvals) {
  const tx = await signer.sendTransaction(approval);
}
```

### Step 4: PermitData (optional)

For this transaction, the user needs to sign to permit Composable Router contract to spend his USDC fist. If using `ethers` package, you can refer to the following code snippet to help the user sign the \`permitData\`:

```typescript
const signer = provider.getSigner(account);
const permitSig = await signer._signTypedData(permitData.domain, permitData.types, permitData.values);
```

After signing, it is necessary to include `permitData` and `permitSig` into `routerData`. Without this step, the transaction will fail.

```typescript
routerData.permitData = estimateResult.permitData;
routerData.permitSig = permitSig;
```
