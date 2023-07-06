# Balancer V2

In this section, we will introduce the Balancer V2 SDK interfaces, which provide developers with a convenient and efficient way to interact with the Balancer V2 protocol. These interfaces cover various aspects of the protocol, including flash loan, and are designed to be easy to use and flexible.

In the following section, we will introduce the interfaces related to the Balancer V2 protocol, which can be accessed through the `api.protocols.balancerv2.` prefix.

## FlashLoan

The following code defines functions related to the Balancer V2 flash loan logic:

### Types

Please refer to the [FlashLoan Logic](flashloan-logic.md) section for more information.

### Functions

* **getFlashLoanTokenList(chainId: number)**: An asynchronous function that retrieves the list of tokens supported by the Balancer V2 flash loan logic on the specified `chainId`.
* **newFlashLoanLogic(fields: FlashLoanFields)**: A function that creates the Balancer V2 flash loan logic data with the given `fields` object.
* **newFlashLoanLogicPair(outputs: FlashLoanFields\['outputs'])**: A function that creates the Balancer V2 flash loan logic data pair with the given `outputs` object.

### Example Code

```typescript
import * as api from '@protocolink/api';

const chainId = 1;

const tokenList = await api.protocols.balancerv2.getFlashLoanTokenList(chainId);
const underlyingToken = tokenList[0];

const outputs = [
  {
    token: underlyingToken,
    amount: '10000',
  },
];

const [flashLoanLoanLogic, flashLoanRepayLogic] = api.protocols.balancerv2.newFlashLoanLogicPair(outputs);
const logics = [flashLoanLoanLogic];
// logics.push(swapLogic)
// logics.push(supplyLogic)
// logics.push(...)
logics.push(flashLoanRepayLogic);
```
