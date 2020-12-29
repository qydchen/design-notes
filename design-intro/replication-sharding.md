## Replication and Sharding

- Replication
  - a duplicate of the main database that will take over the work if the main db shuts down
  - the main database will read and write data, as well as updating the replica
  - you never want the replica to be out of sync with the main db, so if updating to replica fails, then the write operation should fail
    - this means that write operations are a bit more expensive
  - if a user in US writes a post, it gets stored in the US database, and then asynchronously updates the India replica database (maybe every minute, hour, etc)
    - this can improve latency in systems when it comes to read
- Sharding
