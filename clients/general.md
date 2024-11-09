---
order: 1000
---

In `hedwig`, a Client represents a connection to an external, third-party service, such as `AWS S3` or `Redis`, which you can use in distributed workflows. 

### What Does a Client Do?
Clients enable integration with external resources by allowing specific actions, such as storing, retrieving, or modifying data. For each client, `hedwig` manages connections if necessary, performs rollback actions to maintain a consistent state across services in case of an error.

### Supported Clients
Currently, `hedwig` supports -

#### 1. S3 Client
Allows for object storage operations, such as uploading, copying, and deleting files in AWS S3.

#### 2. Redis Client
Supports key-value operations, such as setting and retrieving values in a Redis store.

Each client can be configured with tailored rollback strategies to control how backups and state recovery are managed, ensuring that the distributed transaction maintains reliability across different services.

### Configuring Clients
Clients are easily configured within the Transaction Manager setup. Each client can be customized with specific settings and rollback strategies suited to the transaction’s needs. For more details, please refer to the wanted client page.