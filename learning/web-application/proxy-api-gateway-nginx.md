---
description: >-
  API Gateway acts as a single entry point for multiple APIs and services.
  popular API Gateway includes Amazon API Gateway, NGINX, Apigee (Google Cloud)
---

# \[Proxy] API Gateway (NGINX)

### What API Gateway can do?

An API Gateway is a traffic manager that allows developers to create, publish, maintain, monitor, and secure APIs. It is the intermediary between **client** (usually via frontend, Postman, etc) and **server** (backend micro-services deployed on the cloud)

Advantages of using API Gateway:

* Make APIs more secure through a single entry.
* Enable server side to easily configure the policies of multiple endpoint such as authentication, rate limits, routing, mediation, etc.
* Comprehensive collection of metrics for the API usage analysis.

#### Rate Limiting

Setting Rate limit allow the server to avoid from DDOS Attack. We can say that each IP address can only make 10 API request per seconds, otherwise returning Too Many request error.

#### Authentication

API Key and JWT authentication are common technique to keep endpoint from improper usage. For API key authentication, the API key is sent through header, and the API gateway check whether it matches the allowlist, and return Success 200, Unauthorized 401, Forbidden 403 accordingly.&#x20;

By doing so, the application code does not need to validate API keys itself; instead an API gateway handles the authentication process and routes each request to the appropriate endpoint.

#### Load Balancer

Let's say the product API is **overloaded** and developer want to add server B and server C to handle the high volume request coming through the https://api/products, we can add those servers and configure the load balance strategy such as ip\_hash, random, least connection, weight, to e**nsure the request is distributed optimally.**

#### Monitor and Analytics

Since all incoming request come through the API Gateway, it can keep track of the traffic and usage of multiple API, which could be beneficial for future debigging or analysis

#### Caching

Caching is also a common strategy to lower the response time. When the API is not volatile, we can add different caching strategy to API gateway. For example, `max_size` sets the maximum memory of the cache like 10 GB; `inactive` specifies how long an item can remain in the cache when it is not accessed like 10 minutes;&#x20;

#### Logging

As the API gateway can store any valid and invalid request, it is very convenient to come here and troubleshooting one of the API

#### Routing and endpoint management

Since it simultaneously manages multiple APIs, it can handle where the request is routed to after the request pass the authentication.



### References

[Using NGINX as API Gateway](https://marcospereirajr.com.br/using-nginx-as-api-gateway-7bebb3614e48)

