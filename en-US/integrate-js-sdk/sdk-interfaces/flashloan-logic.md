# FlashLoan Logic

In this guide, we will introduce three main types that are essential for implementing Flash Loan via our SDK, which can be accessed using the `api.` prefix:

* **FlashLoanLogicFields**: This type represents the fields required for Flash Loan logic, including the unique `id`, `outputs` and a boolean `isLoan` field.
* **FlashLoanFields**: A type that represents the fields required for the flash loan logic.
* **FlashLoanLogic**: An interface that extends the `Logic` interface and represents the Aave v3 supply logic. It includes the `id`, `rid`, and `fields` properties.

For any FlashLoan-like logic, you will need to create two FlashLoan logics data **with a unique ID (such as a UUID):**

* one with **`isLoan = true`**, representing the loan taken out from the protocol
* one with **`isLoan = false`**, representing the loan repayment

And additional logics that need to be executed during the FlashLoan process should be wrapped within these two FlashLoan logics.

Remember, the FlashLoan logic with **`isLoan = true`** should be the first one, and the FlashLoan logic with **`isLoan = false`** should be the last one.
