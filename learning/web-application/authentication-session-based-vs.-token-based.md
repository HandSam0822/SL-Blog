---
description: >-
  There're two main type of authentication: session-based and token-based.
  Generally, token based in more secure and reliable. What's their pros and
  cons?
---

# \[Authentication] Session-based vs. token based

### Authentication

Server authenticate that username and password matched&#x20;

### Authorization

Server authorize the action is sent from user who logged in

### Session-based

1. Client request to login -> **Server generate a session id, and store in db** -> client get response and store session in cookie&#x20;
2. Client request to login along with cookie data -> server lookup session id and authorize the login action -> client login

### Token-based (JSON Web Token)

1. Client request to login  -> **Server generate a verified signature(JWT) by hashing data** like header, payload and their combination -> client put JWT into local storage
2. Client appending JWT to header and make login request -> decode the JWT and authorize the client request -> client login

The main difference is that **JWT doesn't store session id in db**, it **encode and decode** client information. It balances the loading of database and allows client to login across difference service. Unlike JWT, session id stored in one server can't be shared with another server.



NOTE: Remember to put expire time as one of the payload field to prevent hacker from hijacking your JWT and use it again and again.

### Reference

[What Is JWT and Why Should You Use JWT](https://www.youtube.com/watch?v=7Q17ubqLfaM)

[Session vs Token Authentication in 100 Seconds](https://www.youtube.com/watch?v=UBUNrFtufWo)

\


\
