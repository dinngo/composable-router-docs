# Utility

In this section, we will cover the functionalities provided by our Utility logics, which includes Multi Send, Send Token, and Wrapped Native Token. These logics are designed to make common operations more streamlined and efficient for developers. Whether you're building a dApp or working on a complex project, our Utility logics can help you save time and improve your workflow.

In the following section, we will introduce the interfaces of Utility logics, which can be accessed through the `api.protocols.utility.` prefix.

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

* **SendTokenLogic**: An interface that extends the `Logic` interface and represents the Utility send token logic. It includes the `id`, `rid`, and `fields` properties.

```typescript
interface SendTokenLogic {
  id: string;
  rid: string;
  fields: SendTokenFields;
}
```

### Functions

* **getSendTokenTokenList(chainId: number)**: An asynchronous function that retrieves the list of tokens supported by the Utility send token logic on the specified chainId.
* **newSendTokenLogic(fields: SendTokenFields)**: A function that creates a new Utility send token logic data with the given fields object.

### Example Code

```typescript
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
