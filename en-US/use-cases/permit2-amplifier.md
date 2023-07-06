# Permit2 Amplifier

A new tech update from **Uniswap,** [**Permit2**](https://docs.uniswap.org/contracts/permit2/overview)**,** allows for token approvals to be shared and managed across different applications, creating a more unified, cost-efficient, and safer UX.

#### Without Permit2

When a user needs to perform trading actions with ERC-20 tokens, they need to send a transaction first to authorize the protocol to access a certain amount of the user's tokens. Additionally, it is common to use 'approve max', which could potentially carry risks in blockchain.

#### With Permit2

The user only needs to authorize the transaction once to permit2 contract. Then, when using an integrated protocol, the token can be used with only a signature within a certain time limit. Now that Uniswap has integrated this mechanism, the user experience has become more seamless and safer. However, any new protocol still requires a new signature, and the number of protocols that use permit2 is still limited.

### Router + Permit2 ✨

By combining Protocolink with permit2 it will greatly improve the user experience and safety. This is achieved through only requiring one signature (also time-limited), and directly using the token to any contract. In addition, the Router does not retain user assets, further enhancing the experience of using the wallet.

