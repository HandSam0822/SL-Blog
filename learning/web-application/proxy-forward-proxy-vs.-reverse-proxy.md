---
description: >-
  Web Proxy acts as an intermediary between client and web server. There're two
  types of proxy server, reverse and forward proxies.
---

# \[Proxy] Forward Proxy vs. Reverse Proxy

### Forward Proxy

Forward proxy sits between client and the Internet and acts on behalf of clients to send request to server.

Use case:&#x20;

1. Control and monitor the internet access (for example: in school's internet, the 18+ content will be blocked)
2. Protect client's online identity because the IP address is unrevealed.

### Reverse Proxy

Reverse proxy receives requests from clients and evenly distributes to servers. The clients are unaware of the actual server that sends the response.

Use Case:&#x20;

1. Load Balance: Distribute incoming traffic among multiple servers in a cluster&#x20;
2. Cache: Cache frequently accessed resources
3. Protect websites: Filtering and blocking malicious traffic.
4. Handle SSL encryption



### References

[Proxy vs Reverse Proxy (Real-world Examples)](https://www.youtube.com/watch?v=4NB0NDtOwIQ)
