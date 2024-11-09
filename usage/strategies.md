---
label: "Strategies"
---

In `hedwig`, each client method used within a transaction has an associated rollback action that will execute automatically if an error occurs during the transaction. We support two rollback strategies that determine how data is backed up before executing: `IN_MEMORY` and `DUPLICATE_FILE`.

### Available Strategies

#### IN_MEMORY
In this strategy, backups are temporarily stored in memory while the transaction is active. For example, if a file is deleted in an S3 bucket, a copy of that file will be kept in memory until the transaction completes. This approach is generally faster, but it requires enough available memory to hold the data being backed up.

#### DUPLICATE_FILE
With this strategy, backups are saved directly in the third-party service. For example, if a file is to be deleted in S3, a duplicate copy of that file is created and saved in a designated backup bucket within S3 until the transaction successfully completes.

### Configuring a Strategy
Each client’s rollback strategy can be configured with a specific `enum` dedicated to that client. This allows you to control the backup approach individually based on the requirements of each transaction.