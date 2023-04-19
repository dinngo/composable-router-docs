---
description: Can be called by Agent to perform additional actions.
---

# Maker Utility

In order to handle special operations that cannot be directly performed by the Agent, such as creating a `CDP` on `Maker`, it is not possible to proceed with operations on this `CDP` in the subsequent steps. Therefore, we have established a **utility** contract specifically designed to handle such special operations, in order to assist users in using the Composable Router system more flexibly. Users can interact directly with the **MakerUtility** contract via Agent to complete the `openLockETHAndDraw()` and `openLockGemAndDraw()` operations.

For detailed sample code, please refer to [this link](https://github.com/dinngo/composable-router-contract/blob/release/v0.1.0-ethtaipei/test/integration/AaveV2.t.sol#L119)

<figure><img src="../../.gitbook/assets/MakerUtility.png" alt=""><figcaption></figcaption></figure>
