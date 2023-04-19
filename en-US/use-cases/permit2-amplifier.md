# Permit2 Amplifier

**Uniswap** released [**Permit2**](https://docs.uniswap.org/contracts/permit2/overview) allows token approvals to be shared and managed across different applications creating a more unified, cost-efficient, and safer UX.

#### Without Permit2

When a user needs to manipulate tokens, needs to send a transaction first to authorize the protocol to access a certain amount of the user's tokens. Additionally, it is common to use 'approve max' which could potentially carry risks in blockchain.

#### With Permit2

The user only needs to authorize the transaction once to permit2 contract, then when using an integrated protocol, the token can be used with only a signature, and with a time limit, now Uniswap has integrated this mechanism, and the experience is great. However, the new protocol still requires a new signature, and the protocol use permit2 is still limited.

### Router + Permit2 ✨

Composable Router combined with permit2 will achieve the characteristic of 1 + 1 > 2. It only requires one signature (also time-limited) and can directly use the token to any contract, making the user experience better. In addition, the Router does not retain user assets, further enhancing the experience of using the wallet.

