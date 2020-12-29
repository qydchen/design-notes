## Load Balancers

Server-Selection Strategy

- how a load balancer chooses servers when distributing traffic amongst multiple servers.
  - round-robin
  - random selection
  - performance-based selection
  - IP-based routing

Hot Spot

- when distributing a workload across a set of servers, that workload might be spread unevenly. This can happen if sharding key or hashing function are suboptimal, or if your workload is naturally skewed: some servers will reeive a lot more traffic than others

Might also make sense to use many load balancers with different server selection strategies
