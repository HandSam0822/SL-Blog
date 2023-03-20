---
description: >-
  SSO is a mechanism enabling clients to login with Identity Provider such as
  Google, Github with no need to create and remember extra set of credential.
---

# \[Authentication] Single Sign-on (SSO)

When a user attempts to access an application or service that requires authentication, the application redirects the user to the IDP's login page.&#x20;

Here's the example of IDP login page

![](<../../.gitbook/assets/image (3).png>)![](<../../.gitbook/assets/image (1).png>)



The user then provides their login credentials to the IDP, which verifies the user's identity and sends a token back to the application. This token is used to authenticate the user and grant them access to the application.&#x20;

There're mainly two types of protocol used for SSO, SAML and OpenID. They both focusing on exchanging authntication and authorization data between an Identiy Provider and a Service Provider, but with different target audience, purpose, and technical implementation.

#### SAML&#x20;

SAML (Security Assertion Markup Language) is primarily designed for **enterprise** use cases and is an XML-based protocol requires more configuration and setup.

#### Open ID

OpenID is more popular in consumer facing applications such as Instagram and Pinterest. It is a JSON-based protocol allowing users to authenticate with third-party provider such as Google or Facebook. It is more simple than SAML.

### What's the role of companies like Okta and Auth0 in SSO?

If you are developing you web app, and desire to provide multiple Identity Provider, it is quite unpleasant to manage login credential from different IDP. Those companies help you store and manage those credential without worrying about security issues.



### Conclusion

By using SSO, the server doesn't need to manage the login credentials anymore, because the responsibility of verifying the user's identity and managing their credentials is delegated to the IDP. This reduces the burden on the server and improves security, because the server no longer needs to store or manage user credentials.



### References

[What Is Single Sign-on (SSO)? How It Works](https://www.youtube.com/watch?v=O1cRJWYF-g4)

