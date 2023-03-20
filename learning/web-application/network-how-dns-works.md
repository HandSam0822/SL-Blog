---
description: >-
  What happen when you type a url and hit enter on the browser? Well, there're
  lots of server being involved in the process including DNS lookup, TCP
  connection, and HTTP request/response.
---

# \[Network] How DNS works?

This article will briefly walk through what's going on when user type a URL with browser, and mainly focus on the **DNS lookup** process.

### What happen when you type a url and hit enter on the browser?

1. Bob enters a URL into the browser
2. Browser looks up IP in cache
3. If no cache, Browser ask DNS resolver to lookup the IP with recursive DNS lookup
4. Browser establishes TCP connection with the server using the IP sent from DNS resolver
5. Browser sends HTTP requests to the server&#x20;
6. Server sends back HTTP response

### How DNS (Domain Name System) works

There're a several name servers sit between client and the server storing those IP address, they're from top to bottom:

1. Recursive DNS resolver (the main role to lookup the domain name)
2. Root Nameserver (holding all address of TLD Name Server)
3. TLD Nameserver (.com, .edu, .uk, etc)
4. Authoritative DNS server (google.com, facebook.com)&#x20;

**Steps in a DNS lookup:**

1. A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a recursive DNS resolver.
2. The resolver sends queries to Root server
3. The root server responds to the resolver with the address of a Top Level Domain (TLD) DNS server. In this case, our request is pointed toward the .com TLD.
4. The resolver then makes a request to the .com TLD.
5. The .com TLD server forward request to authoritative DNS server, where the source of truth locates, and then responds recursive resolver with the IP address
6. Lastly, the recursive resolver responds to the web browser with the IP address (e.g. 8.8.8.8).

It's worth noting that it's not necessary to go through all steps every time because the result will be cached by browser or OS for a period of time.&#x20;



### References

[What is DNS? | How DNS works](https://www.cloudflare.com/learning/dns/what-is-dns/)

[EP 51: How does DNS work?](https://blog.bytebytego.com/p/ep-51-how-does-dns-work)
