---
description: >-
  The one-time address is used for re-entering the Agent. This can only be set
  during contract execution.
---

# Flash Loan Callback

During FlashLoan operations, a callback contract must be provided for the FlashLoan service to call upon, which facilitates the completion of fund management and repayment. In the Composable Router, we have designed state-less, one-time callback contracts specifically for these purposes. if you intend to use a callback contract, you must specify it in the `callback` field of the [`IParam.Logic`](router.md#iparam.logic) struct in advance.

Currently, we support the following:

* [FlashLoanCallbackAaveV2](https://github.com/dinngo/composable-router-contract/blob/release/v0.1.0-ethtaipei/src/FlashLoanCallbackAaveV2.sol)
* [FlashLoanCallbackAaveV3](https://github.com/dinngo/composable-router-contract/blob/release/v0.1.0-ethtaipei/src/FlashLoanCallbackAaveV3.sol)
* [FlashLoanCallbackBalancerV2](https://github.com/dinngo/composable-router-contract/blob/release/v0.1.0-ethtaipei/src/FlashLoanCallbackBalancerV2.sol)

For detailed sample code, please refer to [this link](https://github.com/dinngo/composable-router-contract/blob/release/v0.1.0-ethtaipei/test/integration/AaveV2.t.sol#L119)

<figure><img src="../../.gitbook/assets/callbacks (2).png" alt=""><figcaption></figcaption></figure>



###



