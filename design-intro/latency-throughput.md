Latency - How long it takes for data to traverse from one point in a system to another point in the system

- What is the latency of a client request?
- Rough approximations
  - Reading 1 mb -> 250 µs
  - Reading 1 mb SSD -> 1000 µs
  - Sending 1mb over 1 gb/s to an adjacent network -> 10000µs
  - Reading 1mb HDD -> 20000 µs
  - 1 packet CA to Netherlands and back -> 150000 µs
- Takeaways:
  - Reading is faster than sending data over the network

Throughput - The number of operations that a system can handle properly per time unit. The throughput of a server can often be measured in requests per second (RPS or QPS)

- How to optimize throughput?
  - Pay for it
