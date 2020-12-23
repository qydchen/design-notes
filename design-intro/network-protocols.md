## Network Protocol

Agreed upon set of rules of interaction between two parties

### IP - Internet Protocol

- Modern internet effectively runs on IP
- Data gets sent by IP packets
- `IP Header` section of an IP packet: contains information about the packet
  - 2 versions: IPV 4 (most of modern internet uses) & IPV 6
  - small - between 20 - 60 bytes
- IP data consists of 2^16 bytes => 0.065mb
  - Multiple IP packets in an unordered way

### TCP - Transmission Control Protocol

- Meant to send IP packets in an ordered, reliable way
- Used in all web applications, allows to send arbitrarily long data
- `TCP Header` additional TCP information of the ordering of packets
- More functional, powerful control built on top of IP protocol

### HTTP - HyperText Transfer Protocol

- Protocol that was built on top of TCP
- Introduces a higher level of abstraction above TCP
- Request-response paradigm: 1 machine sends a request to another machine and the other machine returns a response to the machine
- Most modern day ststems rely on modern day systems
- We deal with HTTP request + responses
- Say we have a port in localhost:3000 and a GET /hello resource
  - `curl localhost:3000/hello`
  - `curl --header 'content-type: application/json' localhost:3000/hello --data '{"foo": "bar"}'`
