# 2⃣ Build Logics

Let's start building these logics.

## Swap Logic

The user can swap 1000 USDC for WBTC using the SwapTokenLogic of Uniswap V3.

1. Use `api.protocols.uniswapv3.getSwapTokenQuotation` to get a quotation.
2. Use `api.protocols.uniswapv3.newSwapTokenLogic` to build the swap Logic data.

Below is the code snippet:

```typescript
import * as api from '@furucombo/composable-router-api';
import * as common from '@furucombo/composable-router-common';

const chainId = common.ChainId.mainnet;

const USDC = {
  chainId: 1,
  address: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
  decimals: 6,
  symbol: 'USDC',
  name: 'USD Coin',
};
const WBTC = {
  chainId: 1,
  address: '0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599',
  decimals: 8,
  symbol: 'WBTC',
  name: 'Wrapped BTC',
};

const swapQuotation = await api.protocols.uniswapv3.getSwapTokenQuotation(chainId, {
  input: { token: USDC, amount: '1000' },
  tokenOut: WBTC,
});

const swapLogic = api.protocols.uniswapv3.newSwapTokenLogic(swapQuotation)
```

## Supply Logic

Then you can take the output of the previous `swapQuotation` and use it as an input to get the supply quotation.

1. Use `api.protocols.aavev3.getSupplyQuotation` to get a quote for supplying WBTC, which will essentially provide a 1:1 aEthWBTC.
2. Use `api.protocols.aavev3.newSupplyLogic` to build the supply Logic data.

```typescript
import * as api from '@furucombo/composable-router-api';

const supplyQuotation = await api.protocols.aavev3.getSupplyQuotation(chainId, {
  input: swapQuotation.output,
  tokenOut: aEthWBTC,
});

const supplyLogic = api.protocols.aavev3.newSupplyLogic(supplyQuotation);
```
