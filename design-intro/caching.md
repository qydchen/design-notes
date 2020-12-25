# Caching

Used to reduce or improve the latency of a system

Caching can be done in:

- Client
- Server
- Database

Redis - fast in-memory cache

Cache Eviction Policy
The policy by which values get evicted or removed from a cache.
Popular cache eviction policies include LRU, FIFO, and LFU

Content Delivery Network
A CDN is a third-party service that acts like a cache for your servers. Sometimes, web applications can be slow for users in a particular region if your servers are located only in another region.
A CDN has servers all around the world, meaning that the latency to a CDN's servers will almost always be far better than the latency to your servers. A CDN's servers are often referred to as PoPs (Points of Presence). Two of the most popular CDNs are Cloudflare and Google Cloud CDN
