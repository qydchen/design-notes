## Man-In-The-Middle Attack

An attack in which the attacker intercepts a line of communication that is thought to be private by its two communicating parties.
If a malicious actor intercepted and mutated an IP packet on its way from a client to a server, that would be a man-in-the-middle attack.
MITM attacks are the primary threat that encryption and HTTPS aim to defend against.

## Symmetric Encryption

A type of encryption that relies on only a single key to both encrypt and decrypt data. The key must be known to all parties involved in communcation that must therefore typically be shared between the parties at one point or another.

Symmetric-key algorithms tend to be faster than their asymmetric counterparts.

The most widely used symmetric-key algorithms are part of the Advanced Encryption Standard (AES)

## Asymmetric Encryption

Also known as a public-key encryption asymmetric encrpytion relies on two keys -- a public key and a private key -- to ecnrypt and decrypt data. The keys are gnerated using cryptographic algorithms and are mathematically connected such that data encrypted with the public key can only be decrypted with the private key.

While the private key must be kept secure to maintain the fidelity fo this encrpytion paradigm, the public key can be openly shared.

Asymmetric-key algorithms tend to be slower than their symmetric counterparts.

## AES

Advanced Encryption Standard. AES is a widely used encryption standard that has three symmetric-key algorithms (AES-128, AES-192, and AES-256).

Of note, AES is considered to be the "gold standard" in encrpytionand is even used by the US National Security Agency to encrypt top secret information.

## HTTPS

HyperText Transfer Protocol Secure is an extension of HTTP that's used for secure communcation online. It requires servers to have trusted certificates (usually SSL certificates) and uses the Transport Layer Security (TLS), a security protocol built on top of TCP, to encrpyt data communicated between a client and a server.

## TLS

The Transport Layer Security is a security protocol over which HTTP runs in order to achieve secure communcation online. "HTTP over TLS" is also known as HTTPS.

## SSL Certificate

A digial certificate granted to a server by a certificate authority. Contains the server's public key, to be used as port of the TLS handshake process in an HTTPS connection.

An SSL certificate effectively confirms that a public key belongs to the server claiming it belongs to them. SSL certificates are a crucial defense against man-in-the-middle attacks.

## Certificate Authority

A trusted entity that signs digital certiciates -- namely, SSL certificates that are relied on in HTTPS connections.

## TLS Handshake

The process through which a client and a server communicating over HTTPS exchange encryption-related information and establish a secure communication. The typical steps in a TLS handshake are roughly as follows:

- The client sends a client hello--a string of random bytes--to the server.
- The server responds with a server hello--another string of random bytes-- as well as its SSL certificate, which contains its public key
- The client verifies that the certificate was issued by a certificate authority and sends a premaster secret-- yet another string of random bytes, this time encrypted with the server's public key -- to the server.
- The client and the server use the client hello, the server hello, and the premaster secret to then generate the same symmetric encryption session keys, to be used to encrypt and decrypt all data communicated during the remainder of the connection
