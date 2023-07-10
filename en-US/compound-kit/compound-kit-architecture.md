# 🍀 Compound Kit Architecture

<figure><img src="../.gitbook/assets/Gitbook Architecture Diagram (1).png" alt=""><figcaption><p><strong>Logic:</strong> the above illustrates the actions performed during execution, such as approval, swap, supply, borrow, flash loans, and so on.</p></figcaption></figure>

## Developer

Developers can utilize the Compound Kit SDK into their frontend or backend services. With the use cases supported by the Compound Kit, they can easily generate transaction data or utilize it even for complex transaction scenarios. This significantly lowers the barrier for developers, allowing them to focus on providing a better user experience or infrastructure.

## Compound Kit API/SDK

The Compound Kit API and its SDK generate and return transaction data based on the specified use cases. It provides estimated execution results, calculates the optimal path for each use case, forwards protocol logics to [Protocolink](../why-protocolink.md).
