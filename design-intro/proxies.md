## Proxies

Reverse Proxy

- acts on behalf of a server
- when a client issues a request, the request goes to the reverse proxy and the client wont know that it is going to a reverse proxy
- the dns query returns the ip address of the reverse proxy
- useful
  - use reverse proxy to filter some request
  - take care of logging
  - cache certain html pages
  - load balancer
    - a server that can distribute request load between a bunch of servers
- nginx

(Forward) Proxy

- a server that sits in between a client/set of clients and another server/set of servers
- acts on behalf of client/clients
- if a client wants to communicate with a forward proxy, the client will tell the proxy to communicate on the client's behalf
- a forward proxy can serve as a way to hide the identity of a client, the source IP address is going to be the proxy
