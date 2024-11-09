---
label: "Executing a transaction"
---
This guide walks you through setting up a TransactionManager instance with hedwig for managing distributed workflow and executing your first transaction!

### Create a transaction manager
`TransactionManager` is a class that enables you to set up various connections to third-party services for use within your workflow, allowing you to create and execute distributed transactions. Simply create a new manager instance and configure your desired services. (For detailed information on each service, please refer to the [Clients](../clients/general.md) section.)

```ts
const manager = new TransactionManager({
  s3Config: {
    region: 's3-region',
    endpoint: 's3-endpoint',
    rollbackStrategy: S3RollbackStrategyType.IN_MEMORY,
  },
  redisConfig: {
    url: 'redis-url',
    rollbackStrategy: RedisRollbackStrategyType.IN_MEMORY,
  },
});
```

### Executing a transaction
Once the `TransactionManager` is configured, use it to create and execute a transaction. The transaction method accepts an async function that allows access to different clients for every supported third party service, in the following example - S3Client and RedisClient.

```ts
  await manager.transaction(async ({ S3Client, RedisClient }) => {
    if (S3Client) {
      await S3Client.putObject({
        Bucket: 'my-local-bucket',
        Key: 'key',
        Body: Buffer.from('value', 'utf-8'),
      });
    }

    if (RedisClient) {
      await RedisClient.set('key', 'value');
    }
  });
};
```

You can use the different supported methods of every client as specifid in the [Clients](../clients/general.md) section.

### Rolling back
If an error occurs during the transaction, the rollback procedure will initiate. For more details on the various rollback approaches, please refer to the [Strategies](./strategies.md) page.