# \[Authentication] OAuth

1. The user wants to access a service or resource (such as posting a message on Facebook or retrieving contacts from Google).
2. The third-party application (client) requests authorization to access the user's resources. This request contains a client ID and a callback URL.
3. The authorization server authenticates the user and asks them to grant permission to the client.
4. If the user grants permission, the authorization server generates an access token and sends it to the client.
5. The client can now use the access token to make requests to the resource server on behalf of the user.
6. The resource server validates the access token and responds with the requested data.
7. The client can continue to make requests to the resource server until the access token expires or is revoked.
