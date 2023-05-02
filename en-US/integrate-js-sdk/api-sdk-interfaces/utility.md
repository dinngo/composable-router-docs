# Utility

In this section, we will cover the functionalities provided by our Utility logics, which includes Multi Send, Send Token, and Wrapped Native Token. These logics are designed to make common operations more streamlined and efficient for developers. Whether you're building a dApp or working on a complex project, our Utility logics can help you save time and improve your workflow.

In the following section, we will introduce the interfaces of Utility logics, which can be accessed through the `api.protocols.utility.` prefix.

## WrappedNativeToken

The following code defines interfaces and functions related to the Utility wrapped native token logic:

### Types

* **WrappedNativeTokenParams**: A type that represents the input parameters for the Utility wrapped native token logic

```typescript
interface WrappedNativeTokenParams {
  input: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  };
  tokenOut: {
    chainId: number;
    address: string;
    decimals: number;
    symbol: string;
    name: string;
  };
}
```

* **WrappedNativeTokenFields**: A type that represents the fields required for the Utility wrapped native token logic.

```typescript
interface WrappedNativeTokenFields {
  input: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  };
  output: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  };
}
```

* **WrappedNativeTokenLogic**: An interface that extends the `Logic` interface and represents the Utility wrapped native token logic. It includes the `rid`, and `fields` properties.

```typescript
interface WrappedNativeTokenLogic {
  rid: string;
  fields: WrappedNativeTokenFields;
}
```

### Functions

* **getWrappedNativeTokenTokenList(chainId: number)**: An asynchronous function that retrieves the list of tokens supported by the Utility wrapped native token logic on the specified `chainId`.
* **getWrappedNativeTokenQuotation(chainId: number, params: WrappedNativeTokenParams)**: An asynchronous function that retrieves a quotation for wrapping or unwrapping native token with the specified `params` object on the specified `chainId`.
* **newWrappedNativeTokenLogic(fields: WrappedNativeTokenFields)**: A function that creates the Utility wrapped native token logic data with the given `fields` object.

### Example Code

```typescript
import * as api from '@furucombo/composable-router-api';

const chainId = 1;

const tokenList = await api.protocols.utility.getWrappedNativeTokenTokenList(chainId);

// wrap: native token to wrapped native token
const wrapTokenIn = tokenList[0][0]; // native token
const wrapTokenOut = tokenList[0][1]; // wrapped native token

const wrapQuotation = await api.protocols.utility.getWrappedNativeTokenQuotation(chainId, {
  input: {
    token: wrapTokenIn,
    amount: '10',
  },
  tokenOut: wrapTokenOut,
});

const wrapLogic = await api.protocols.utility.newWrappedNativeTokenLogic(wrapQuotation);

// unwrap: wrapped native token to native token
const unwrapTokenIn = tokenList[1][0]; // wrapped native token
const unwrapTokenOut = tokenList[1][1]; // native token

const unwrapQuotation = await api.protocols.utility.getWrappedNativeTokenQuotation(chainId, {
  input: {
    token: unwrapTokenIn,
    amount: '10',
  },
  tokenOut: unwrapTokenOut,
});

const unwrapLogic = await api.protocols.utility.newWrappedNativeTokenLogic(unwrapQuotation);
```

## SendToken

The following code defines interfaces and functions related to the Utility send token logic:

### Types

* **SendTokenFields**: A type that represents the fields required for the Utility send token logic.

```typescript
interface SendTokenFields {
  input: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  };
  recipient: string;
}
```

* **SendTokenLogic**: An interface that extends the `Logic` interface and represents the Utility send token logic. It includes the `rid`, and `fields` properties.

```typescript
interface SendTokenLogic {
  rid: string;
  fields: SendTokenFields;
}
```

### Functions

* **getSendTokenTokenList(chainId: number)**: An asynchronous function that retrieves the list of tokens supported by the Utility send token logic on the specified chainId.
* **newSendTokenLogic(fields: SendTokenFields)**: A function that creates the Utility send token logic data with the given fields object.

### Example Code

```typescript
import * as api from '@furucombo/composable-router-api';

const chainId = 1;

const tokenList = await api.protocols.utility.getSendTokenTokenList(chainId);
const tokenIn = tokenList[0];

const sendTokenLogic = await api.protocols.utility.newSendTokenLogic({
  input: {
    token: tokenIn,
    amount: '10',
  },
  recipient: '0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa',
});
```

## MultiSend

The following code defines interfaces and functions related to the Utility multi-send logic:

### Types

* **MultiSendFields**: A type that represents the fields required for the Utility multi-send logic.

```typescript
type MultiSendFields = {
  input: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  };
  recipient: string;
}[];
```

* **MultiSendLogic**: An interface that extends the `Logic` interface and represents the Utility multi-send logic. It includes the `rid`, and `fields` properties.

```typescript
interface MultiSendLogic {
  rid: string;
  fields: MultiSendFields;
}
```

### Functions

* **getMultiSendTokenList(chainId: number)**: An asynchronous function that retrieves the list of tokens supported by the Utility multi-send logic on the specified chainId.
* **newMultiSendLogic(fields: MultiSendFields)**: A function that creates the Utility multi-send logic data with the given fields object.

### Example Code

```typescript
import * as api from '@furucombo/composable-router-api';

const chainId = 1;

const tokenList = await api.protocols.utility.getMultiSendTokenList(chainId);
const tokenA = tokenList[0];
const tokenB = tokenList[1];

const multiSendLogic = await api.protocols.utility.newMultiSendLogic([
  {
    input: {
      token: tokenA,
      amount: '10',
    },
    recipient: '0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa',
  },
  {
    input: {
      token: tokenB,
      amount: '10',
    },
    recipient: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
  },
  ...
]);
```

## CustomData

If you want to interact with protocols that are not currently supported by our SDK, you can combine the intended transaction `to` and `data`, along with the amount of tokens to be spent and received, to create the Utility custom data logic data. And you can also use this with our supported protocols.

The following code defines interfaces and functions related to the Utility custom data logic:

### Types

* **CustomDataFields**: A type that represents the fields required for the Utility custom data logic.

```typescript
interface CustomDataFields {
  inputs?: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  }[];
  outputs?: {
    token: {
      chainId: number;
      address: string;
      decimals: number;
      symbol: string;
      name: string;
    };
    amount: string;
  }[];
  to: string;
  data: string;
}
```

* **CustomDataLogic**: An interface that extends the `Logic` interface and represents the Utility custom data logic. It includes the `rid`, and `fields` properties.

```typescript
interface CustomDataLogic {
  rid: string;
  fields: CustomDataFields;
}
```

### Functions

* **newCustomDataLogic(fields: CustomDataFields)**: A function that creates the Utility custom data logic data with the given fields object.

### Example Code

```typescript
import * as api from '@furucombo/composable-router-api';
import * as common from '@furucombo/composable-router-common';
import axios from 'axios';

const chainId = 1;
const account = '0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa';

const fromToken = {
  chainId: 1,
  address: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
  decimals: 6,
  symbol: 'USDC',
  name: 'USD Coin',
};
const toToken = {
  chainId: 1,
  address: '0x6B175474E89094C44Da98b954EedeAC495271d0F',
  decimals: 18,
  symbol: 'DAI',
  name: 'Dai Stablecoin',
};
const input = new common.TokenAmount(fromToken, '100');

const { data } = await axios.get(`https://api.1inch.io/v5.0/${chainId}/swap`, {
  params: {
    fromTokenAddress: fromToken.address,
    toTokenAddress: toToken.address,
    amount: input.amountWei.toString(),
    fromAddress: account,
    slippage: 1,
    disableEstimate: true,
  },
});
const output = new common.TokenAmount(toToken).setWei(data.toTokenAmount);

const customDataLogic = await api.protocols.utility.newCustomDataLogic({
  inputs: [input],
  outputs: [output],
  to: data.tx.to,
  data: data.tx.data,
});
```