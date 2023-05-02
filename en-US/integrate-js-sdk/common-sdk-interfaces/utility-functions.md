# Utility Functions

This section contains utility functions that can be used to perform various common operations in dApp development.

* `toSmallUnit`: Converts an amount in decimal units to an amount in the smallest unit of a token, given the number of decimal places. Returns a BigNumber.
* `toBigUnit`:&#x20;
  * Converts an amount in the smallest unit of a token to an amount in decimal units, given the number of decimal places. Returns a string.
  * options (optional) is an object that can contain the following properties:
    * displayDecimals (optional): number of decimal places to include in the output string (default is the given decimals).
    * mode (optional): rounding mode to use ('ceil', 'round', or 'floor', default is 'floor').
* `calcSlippage`: Calculates the maximum amount of slippage, given an amount and a slippage percentage. base (optional) is the base number used to calculate slippage (default is 10000).
* `calcFee`: Calculates the amount of a fee, given an amount and a premium percentage. base (optional) is the base number used to calculate slippage (default is 10000).
* `calcAmountBps`: Calculates the amount of an asset as a basis point of the total balance.
* `shortenAddress`: Shortens an address to a specified number of digits (default is 4).
* `shortenTransactionHash`: Shortens an transaction hash to a specified number of digits (default is 4).
