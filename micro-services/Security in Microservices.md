
Security in Microservices
========================



Why Basic Authentication is not suitable in Microservices Context?
-------

Basic Authentication is natively supported by almost all servers and clients, even Spring security has very good support for it and its configured out of the box. But it is not a good fit for Microservices due to many reasons, including -
1. We need credentials (username and password) every time we authenticate. This may be fine where all the participants can share the secrets securely, but Users may not be willing to share their credentials with all the applications.
2. There is no distinction between Users and Client Apps (application that is making request). In a realistic environment, we often need to know if a real user is making request or a client app is making request (for inter service communication).
3. It only covers authentication. what about scopes, Authorizations? Basic Auth does not support adding additional attributes in the authentication headers. There is no concept of Tokens in basic auth.
4. Performance reasons for BCrypt Matching. Passwords are often stored in database using one way hash i.e. Bcrypt, it takes lot of cpu cycles dependening upon the strength (a.k.a. log rounds in BCrypt) to compare the user’s plain password with db saved bcrypt password, so it may not be a efficient to match password on every request. The larger the strength parameter the more work will have to be done(exponentially) to hash the passwords. If you set strength to 12, then in total 212 iterations will be done in Bcrypt Logic. Usually 4-8 passwords can be matched per second on a T2.Micro instance on Amazon AWS instance. See BCryptPasswordEncoder 
for more info.
   https://docs.spring.io/springsecurity/site/docs/4.0.4.RELEASE/apidocs/org/springframework/security/crypto/bcrypt/BCryptPasswordEncoder.html
5. If we use Basic Auth for a mobile application client, then we might have to store user’s credentials on the device to allow remember me feature. This is quite risky as anyone getting access to device may steal the plain credentials.

Why OAuth2?
-------

1. Simple for Clients (client is often a microservice itself)
2. AcessTokens can carry information beyond identity (like clientId, roles, issuer, userid, resourceId, expiry, scope, etc.).
3. Distributed and Stateless. You can validate the token’s authenticity yourself.
4. Refresh Token support
5. Clear distinction between user and machines.
6. Lightweight
7. A client application, often web application, acts on behalf of user, but with user’s approval.
8. Interoperability with non-browser clients.

OAuth2.0 is a delegation protocol where the Client (Mobile App or web app) does not need to know about the credentials of Resource Owner (end user).

OAuth2 Roles
-------
 <img src="./images-ms/Four different roles in OAuth 2.0 protocol.png" width="800" border="2" />

Oauth2 defines four roles.
1. **Resource Owner** - The person or the application that owns the data to be shared. When resource owner is a person, it is called as an end-user.
2. **Resource Server** - The application that holds the protected resources. It is usually a microservice.
3. **Authorization Server** - the application that verifies the identity of the resource owner(users/clients). This server issues access tokens after obtaining the authorization.
4. **Client** - the application that makes request to Resource Server on behalf of Resource Owner. It could be a mobile app or a web app (like stackoverflow).

OAuth 2.0 grant types (OAuth flows)
-------



When shall I use resource owner credentials?
-------




When shall I use Authorization Code grant?
-------



When shall I use client credentials?
-------



OAuth2 and Microservices
-------




What is JWT?
-------


What are use cases for JWT?
-------


How does JWT looks like?
-------


What is AccessToken and RefreshToken?
-------




How to use a RefreshToken to request a new AccessToken?
-------


How to call the protected resource using AccessToken?
-------


Can a refreshToken be never expiring? How to make refreshToken life long valid?
-------



Generate AccessToken for Client Credentials.
-------


Why there is no RefreshToken support in Oauth2 Client Credentials workflow?
-------


