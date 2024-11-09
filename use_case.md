---
label: "Use Case"
icon: search
order: 1001
---

## What is `hedwig`

In modern distributed systems, workflows frequently involve interacting with multiple third-party services like databases, object storage, and caching layers. Each of these services can have their own latency, reliability, and error characteristics, which complicates workflow consistency and data integrity across different parts of a transaction.

`hedwig` is designed to ensure that transactions involving multiple external resources are managed consistently and efficiently. 

## Example

Imagine a workflow where you need to upload a receipt to `S3` and save order details in a `Redis` cache. With `hedwig`, you can manage these operations within a single distributed transaction, ensuring a rollback if any part fails -

```mermaid
flowchart TD
    subgraph Transaction
        start((Start)) --> S3[Upload Receipt to S3]
        S3 --> Redis[Cache Order in Redis]
    end
    
    S3 -->|Error| HedwigRollback[Hedwig Rollback Process]
    Redis -->|Error| HedwigRollback
    HedwigRollback --> Restore[Restored State]
    
    Redis --> SuccessEnd((Success))
    
    style Transaction stroke:#4d9,stroke-width:4px;
    style HedwigRollback stroke:orange,stroke-width:4px;
    style Restore stroke:orange,stroke-width:4px;
    style SuccessEnd stroke:#4d9,stroke-width:4px;
```