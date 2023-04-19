# 4⃣ Estimate Router Data

Next, use `api.estimateRouterData` to estimate how much funds will be spent (funds) and how many balances will be obtained (balances) from this transaction. It will also identify any approvals that the user needs to execute (approvals) before the transaction and whether there is any permit2 data that the user needs to sign before proceeding (permitData).

```typescript
import * as api from '@furucombo/composable-router-api';

const estimateResult = await api.estimateRouterData(routerData);
```

The structure of the `estimateResult` obtained is roughly as follows:

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

### funds

For this transaction, `1000 USDC` will be spent, which can be displayed on the interface.

### balances

For this transaction, `0.03579397 aEthWBTC` will be obtained, which can be displayed on the interface.

### approvals

For this transaction, the user needs to approve Permit2 contract to spend his USDC first. If using `ethers` package, you can refer to the following code snippet to help the user send approval transactions:

```typescript
const signer = provider.getSigner(account);
for (const approval of estimateResult.approvals) {
  const tx = await signer.sendTransaction(approval);
}
```

### permitData

For this transaction, the user needs to sign to permit Composable Router contract to spend his USDC. If using `ethers` package, you can refer to the following code snippet to help the user sign the \`permitData\`:

```typescript
const signer = provider.getSigner(account);
const permitSig = await signer._signTypedData(permitData.domain, permitData.types, permitData.values);
```

After signing, it is necessary to include `permitData` and `permitSig` into `routerData`. Without this step, the transaction will fail.

```typescript
routerData.permitData = estimateResult.permitData;
routerData.permitSig = permitSig;
```
