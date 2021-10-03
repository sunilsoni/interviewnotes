
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

An authorization grant is a credential representing the resource owner’s authorization (to access its protected resources) used by the client to obtain an access token.

 <img src="./images-ms/Five Grants in OAuth 2.0 protocol.png" width="800" border="2" />

OAuth2 specification defines four grant types.
1. **Authorization Code** - its mostly used by web applications.
2. **Resource Owner Password Credentials** - It is used mostly by trusted clients like Android/Mobile Apps.
3. **Implicit** - Angular JS Applications and Mobile Apps where clientId and clientSecret can not be kept secret.
4. **Client Credentials** - mostly used for inter service communication by service clients.
5. **Refresh Token** - Used for generating a refresh token

When shall I use resource owner credentials?
-------
When end user is a human, then resource resource owner credentials grant should be used. Important thing to note here is that resource owner’s credentials will be exposed to the client application. Thus it should only be used where client app is trusted application. For example, if you have your own inhouse oauth 2.0 server, then you can use resource owner credentials in your company’s android app.

But if you are integrating with Google or Facebook, then this type of grant is not feasible, because end user will never trust your android app to enter Google’s credentials. Authorization Code grant is better alternative to such scenarios. Using Curl to get Access Token based on password grant_type..

> curl https://clientId:clientSecret@api.host.com/uaa/oauth/token -d grant_type=password -d username=<username> -d password=<password> -d scope=openid

Sample Response.

```json
{
   "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiI4NTkyM2RkZS0yNDIzLTRiYTMtOGN
   "expires_in": 2628000,
   "jti": "9114270c-ea4e-4814-a5b2-3f3e99dc4233",
   "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiI4NTkyM2RkZS0yNDIzLTRiYTMtOG
   "scope": "read",
   "token_type": "bearer",
   "uid": "85923dde-2423-4ba3-8ca9-a833f6b80d83"
}
```


When shall I use Authorization Code grant?
-------
It should be used in applications where clientId and clientSecret can be kept securely i.e. webapps. In this flow the oauth 2.0 client is redirected back to authorization server’s url for authentication purpose.

This grant type is used when you want to integrate with Google/Facebook on your server side webapp.


When shall I use client credentials?
-------
Client credentials should be used for inter service communication that is not on behalf of users i.e. scheduled batch jobs, reporting jobs etc. Unlike Basic Auth, OAuth 2.0 protocol distinguishes between User (Resource Owner) and Machines (Client) based on Resource Owner Credentials and Client Credentials. Thus if the end consumer of your web services is not a human, then client credentials should be used.

Using Client Credentials to generate Access Token.
> curl service-account-1:service-account-1-secret@localhost:8080/auth/oauth/token -d grant_type=client_credentials

OAuth2 and Microservices
-------

 <img src="./images-ms/OAuth2 Use in Microservices Context.png" width="800" border="2" />

1. Resource Servers are often microservices.
2. Web App Clients uses Authorization Code Grant.
3. Browser Clients (single page apps - angular JS, etc) uses Authorization Code Grant or implicit Grant.
4. Mobile App and non-browser clients uses - password grant.
5. Service Clients (intra-system) uses - client credentials or relay user tokens depending upon the requirements.

What is JWT?
-------
JWT is acronym for JSON Web Token. JWT are an open, industry standard RFC 7519 method for representing claims securely between two parties (even on unsecured networks).

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and selfcontained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA.

There are two important points here -

1. JWT are compact so they can be sent through a URL, preferrably as a POST paramater or inside HTTP header.
2. JWT contains all the required data about the user, so there is no need to query the database more than once (once during JWT generation).
3. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are.

**Sources**
https://tools.ietf.org/html/rfc7519
https://jwt.io/introduction/

What are use cases for JWT?
-------
There are many useful scenarios for leveraging power of JWT 

**Authentication**

Authentication is one of the most common scenario for using JWT, specifically in microservices architecture (but not limited to it). In microservices, oauth2 server generates a JWT at the time of login and all subsequent requests can include the JWT AccessToken as the means for authentication.

Implementing Single Sign On by sharing JWT b/w different applications hosted in
different domains.

Information Exchange

JWT can be signed, using public/private key pairs, you can be sure that the senders are who they say they are. Hence JWT is a good way of sharing information between two parties. Example usecase could be -
1. Generating Single Click Action Emails e.g. Activate your account, delete this comment, add this item to favorites, Reset your password, etc. All required information for the action can be put into JWT.
2. Timed sharing of a file download using a JWT link. Timestamp can be part of claim, so when the server time is past the time coded in JWT, link will automatically expire.

How does JWT looks like?
-------
There are 3 parts in every JWT claim - Header, Claim and Signature. These 3 parts are separated by a dot. The entire JWT is encoded in Base64 format.

> JWT = {header}.{payload}.{signature}

A typical JWT is shown here for reference.

**Encoded JSON Web Token**
Entire JWT is encoded in Base64 format to make it compatibel with HTTP protocol. Encoded JWT looks like the following:

 <img src="./images-ms/Encoded JWT Claim.png" width="800" border="2" />


**Decoded JSON Web Token**

**Header** : Header contains algorithm information e.g. HS256 and type e.g. JWT

`Header Part.`

```json
{
"alg": "HS256",
"typ": "JWT"
}
```
**Claim** : claim part has expiry, issuer, user_id, scope, roles, client_id etc. It is encoded as a JSON object. You can add custom attributes to the claim. This is the information that you want to exchange with the third party.

Claim Part.
```json
 {
   "uid": "2ce35360-ef8e-4f69-a8d7-b5d1aec78759",
   "user_name": "user@mail.com",
   "scope": ["read"],
   "exp": 1520017228,
   "authorities": ["ROLE_USER","ROLE_ADMIN"],
   "jti": "5b42ca29-8b61-4a3a-8502-53c21e85a117",
   "client_id": "acme-app"
}
```

**Signature** : Signature is typically a one way hash of (header + payload), is calculated using HMAC  : SHA256 algorithm. The secret used for signing the claim should be kept private.  : Pubic/private key can also be used to encrypt the claim instead of using symmetric  : cryptography.

Signature Part
> HMACSHA256(base64(header) + "." + base64(payload), "secret")

Tip: You can decode and test JWT using https://jwt.io . This is helpful for testing and debugging purpose


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


