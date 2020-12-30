## Peer to Peer

Transfering 5 gb file to 1000 machines at 5 gb/s throughput will take 1000 seconds for 1000 machines.

How can we improve? Instead of 1 machine, use multiple machines.

Suppose 10 machines serving 5 gb file, then it will be 100 seconds per machines, but that is still too slow as it has to replicate files to the other 9 machines.

Suppose sharding? That would not work as there could be a hotpath shard, and that could also then cause the bottleneck

### Solution

5 gb file, split it up to very small chunks, and send it to all of the peers, and then each peer will grab from each other to construct the 5 gb file

1000 machines, each with 5 mb file. A single machine will take 0.999 seconds to grab the rest of the 5 gb file from the 999 other machines.

The idea is that this can parallellize the transfer of 5gb files.
