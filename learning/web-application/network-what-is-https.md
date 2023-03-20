---
description: >-
  HTTPS is a protocol used to encrypt data sent over the internet to provide a
  secure communication between a client (e.g. web browser) and a server (e.g.
  website).
---

# \[Network] What is HTTPS

HTTPS uses a combination of two protocols: HTTP (Hypertext Transfer Protocol) and SSL/TLS (Secure Sockets Layer/Transport Layer Security).

Here's a simplified illustration of how HTTPS works:

1. A client (e.g. web browser) initiates a connection to a server (e.g. website) using the HTTPS protocol.
2. The server responds with its SSL/TLS certificate, which includes a public key and a private key.
3. The client verifies the server's SSL/TLS certificate to ensure that it is valid and issued by a trusted certificate authority.
4. The client generates a random symmetric key, which will be used to encrypt and decrypt the data exchanged between the client and server.
5. The client encrypts the symmetric key with the server's public key, and sends it to the server.
6. The server decrypts the symmetric key using its private key, and establishes a secure connection with the client.
7. The client and server exchange encrypted data over the secure connection using the symmetric key.
8. At the end of the session, the client and server exchange a final message to close the connection.

By encrypting the data exchanged between the client and server, HTTPS helps to prevent eavesdropping, tampering, and forgery of data. It is commonly used for secure online transactions, such as online banking, e-commerce, and online payments, as well as for securing sensitive information, such as passwords and personal information, transmitted over the internet.

#### Why using both symmetric and asymmetric encryption?

Because asymmetric encryption is computationally expensive, and it's not suitable for transmitting bulk data.



### References

[SSL, TLS, HTTPS Explained](https://www.youtube.com/watch?v=j9QmMEWmcfo)\
