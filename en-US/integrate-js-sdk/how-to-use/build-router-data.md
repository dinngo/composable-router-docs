# 3⃣ Build Router Data

Next, you need to prepare the Router Data, which will include the `chainId`, `account`, `logics`, and `slippage` data. By default, the slippage is optional and set to 1%. However, if you want to customize the slippage, you should specify it as a number, using Basis Points where 1 Basis Point equals 0.01%.

```typescript
import * as api from '@furucombo/composable-router-api';

const routerData: api.RouterData = {
  chainId,
  account: '0xaAaAaAaaAaAaAaaAaAAAAAAAAaaaAaAaAaaAaaAa',
  logics: [swapLogic, supplyLogic],
  slippage: 300, // 3%
};
```

