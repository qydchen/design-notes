## Replication and Sharding

- Replication
  - a duplicate of the main database that will take over the work if the main db shuts down
  - the main database will read and write data, as well as updating the replica
  - you never want the replica to be out of sync with the main db, so if updating to replica fails, then the write operation should fail
    - this means that write operations are a bit more expensive
  - if a user in US writes a post, it gets stored in the US database, and then asynchronously updates the India replica database (maybe every minute, hour, etc)
    - this can improve latency in systems when it comes to read
- Sharding

  - split up database into little databases into shards(aka partitions)
  - how to split up the data?
    1. split up tables to store rows into different shards
    2. split up tables by alphabetical order
    3. split up by geographic region
  - how to deal with hotspots?
    1. far fewer customers with X, Y, Z... what to do?
    2. shard by some form of unique id, or some randomly generated username
    3. reasonable way is to use a hashing function to determine which shard

Have replica of each shard, with each replica updated asynchronously. Use a load balancer to determine which shard to update.
