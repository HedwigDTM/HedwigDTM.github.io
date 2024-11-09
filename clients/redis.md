The Redis Client in `hedwig` provides a straightforward way to interact with Redis, a fast, in-memory data store used frequently for caching, session management, and real-time analytics.

## Redis Client Configuration
To configure the Redis Client, provide an object of type `RedisConfig`, which extends `RedisClientOptions` from the [redis](https://www.npmjs.com/package/redis) package. Additionally, you can specify:

* `rollbackStrategy` (optional) – Defines the rollback approach used during transaction errors (either IN_MEMORY or DUPLICATE_FILE)
* `backupHashName` (optional) – Specifies the Redis hash name used for backups when using the DUPLICATE_FILE strategy.

```typescript
export type RedisConfig = RedisClientOptions & {
  rollbackStrategy?: RedisRollbackStrategyType; // IN_MEMORY or DUPLICATE_FILE
  backupHashName?: string;
};
```

## Available Actions
`hedwig`'s Redis Client supports the following actions:

* `get`: Retrieves the value of a specified key.
* `set`: Sets a value for a specified key.
* `del`: Deletes a specified key.
* `incr`: Increments the integer value of a specified key by one.
* `decr`: Decrements the integer value of a specified key by one.

These actions enable easy interaction with Redis, and each action supports rollback strategies to ensure transactional consistency across workflows.