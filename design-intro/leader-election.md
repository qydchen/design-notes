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
