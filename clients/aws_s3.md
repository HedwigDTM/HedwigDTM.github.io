---
label: "AWS S3"
---

The S3 Client in `hedwig` allows integration with Amazon S3, Amazon's scalable storage solution for storing and retrieving any amount of data.

## S3 Client Configuration
To configure the S3 Client, pass an object of type `S3Config`, which extends `S3ClientConfig` from the [@aws-sdk/client-s3](https://npmjs.com/package/@aws-sdk/client-s3) package. You can also specify:

* `rollbackStrategy` (optional) – Determines the rollback behavior when an error occurs (either IN_MEMORY or DUPLICATE_FILE).
* `backupBucketName` (optional) – Specifies the S3 bucket used for file backups when using the DUPLICATE_FILE rollback strategy.

```typescript
export type S3Config = S3ClientConfig & {
  rollbackStrategy?: S3RollbackStrategyType; // IN_MEMORY or DUPLICATE_FILE
  backupBucketName?: string;
};
```
## Available Actions
`hedwig`'s S3 Client supports the following actions:

* `putObject`: Uploads a file to a specified bucket with a specified key.
* `deleteObject`: Removes an object from a bucket.
* `deleteBucket`: Deletes an entire bucket.
* `getObject`: Retrieves an object from a bucket.
* `listBuckets`: Lists all buckets available to the S3 client.
* `headObject`: Checks the metadata of a specified object.
* `headBucket`: Checks if a specific bucket exists and is accessible.

Each of these actions allows for safe interactions with S3 and supports rollback strategies to maintain transaction integrity.