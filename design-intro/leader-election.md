## Leader Election

The process by which nodes in a cluster (for instance, servers in a set of servers) elect a so-called "leader" amongst them, responsible for the primary operations of the service that these nodes support. When correctly implemented, leader election guarantees that all nodes in the cluster know which one is the leader at any given time and can elect a new leader if the leader dies for whatever reason.

Suppose there is a Third-Party Service, and you need a service in between your database. If this service is replicated, leader-election is used to find a server to take over the task.

Leader-election is difficult. The act of having multiple machines to gain consensus is difficult (sharing some state).

### Consensus Algorithms

algorithms that allow multiple nodes in a cluster to agree on some data value

Paxos or Raft - a consensus algorithm

Zookeeper + Etcd - allows to implement leader-election

Etcd - highly available + strong consistency

- uses a consensus algorithm (Raft)
- multiple machines that read and write and uses a main machine that is the single source of truth
- the leader (main) is responsible for all of the writes

### Advantages and disadvantages of leader election

// From AWS

Leader election is a common pattern in distributed systems because it has some significant advantages:

• A single leader makes systems easier for humans to think about. It puts all the concurrency in the system into a single place, reduces partial failure modes, and adds a single place to look for logs and metrics.
• A single leader can work more efficiently. It can often simply inform other systems about changes, rather than building consensus about the changes to be made.
• Single leaders can easily offer clients consistency because they can see and control all the changes made to the state of the system.
• A single leader can improve performance or reduce cost by providing a single consistent cache of data which can be used every time.
• Writing software for a single leader may be easier than other approaches like quorum. The single leader doesn’t need to consider that other systems may be working on the same state at the same time.

Leader election also has some considerable downsides:

• A single leader is a single point of failure. If the system fails to detect or fix a bad leader, the whole system can be unavailable.
• A single leader means a single point of scaling, both in data size and request rate. When a leader-elected system needs to grow beyond a single leader, it requires a complete re-architecture.
• A leader is a single point of trust. If a leader is doing the wrong work with nobody checking it, it can quickly cause problems across the entire system. A bad leader has a high blast radius.
• Partial deployments may be hard to apply in leader-elected systems. Many software safety practices at Amazon depend on partial deployments, such as one-box, A-B testing, blue/green deployment, and incremental deployment with automatic rollback.

Many of these disadvantages can be mitigated by carefully choosing the leader’s scope. How much of the system or data does the leader own? A common pattern here is sharding. Each item of data still belongs to a single leader, but the whole system contains many leaders. This is the fundamental design approach behind Amazon DynamoDB (DynamoDB), Amazon Elastic Block Store (Amazon EBS), Amazon Elastic File System (Amazon EFS), and many other systems at Amazon. Sharding has its own downsides, though. Specifically, more design complexity and the need to carefully think through how to shard data.

### How Amazon elects a leader

There are many ways to elect a leader, ranging from algorithms like Paxos, to software like Apache ZooKeeper, to custom hardware, to leases. Leases are the most widely used leader election mechanism at Amazon. Leases are relatively straightforward to understand and implement, and they offer built-in fault tolerance. Leases work by having a single database that stores the current leader. Then, the lease requires that the leader heartbeat periodically to show that it’s still the leader. If the existing leader fails to heartbeat after some time, other leader candidates can try to take over.

We avoid depending on time in distributed systems, even with the great time sync feature in Amazon Elastic Compute Cloud (Amazon EC2). It’s difficult to ensure that system clocks across a cluster are synchronized enough to depend on that synchronization for ordering or coordinating distributed operations. In Amazon, distributed systems only use time for human consumption. Leases depend on time. However, they depend only on local elapsed time duration, rather than a wall-clock time that is synchronized and needs to be agreed upon by multiple servers.

The DynamoDB lock client source code offers examples and details related to leader election. However, we’ve found that, although leases and locks are conceptually simple, correct implementation can be subtle. Implementations require an understanding of how a server is measuring local time duration. For example, if a server or library that measures time thought that time jumped backwards occasionally, it would break the assumptions about time durations that are built into leases. Durations sidestep problems with global clock synchronization that cause servers to stop agreeing on what time it is, from leap seconds to local clock drift over time from sustained high CPU utilization.

A larger issue for leases, and all kinds of distributed locks, is making sure that the leader is only doing work while it holds the lock. Ensuring that the leader holds the lock is actually fairly hard. We’ve found it important to ensure that a leader on a slow or lossy network doesn't believe that it’s holding locks longer than it really is. Similarly, garbage collection pauses between a lock being checked and work being done can lead to incorrect behavior. In practice, hardening against these issues is often the biggest challenge.

DynamoDB and ZooKeeper offer simple lease-based locking clients which provide fault-tolerant leader election. Unless there are particular needs, we prefer these clients as we think they provide the easiest and most tested way to implement leader election. Amazon teams prefer to avoid creating a custom leader election implementation. Instead, we favor existing clients that are well-tested and battle-hardened.
