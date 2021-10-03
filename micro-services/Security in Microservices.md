
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
In OAuth2, we receive two kind of tokens against authentication - AccessToken[mandatory] and RefreshToken[optional].

JWT Access token is used to authenticate against protected API resources.

JWT Refresh token is used to acquire new Access Token. Token refresh is handled by the following API endpoint: /api/auth/token. Refresh token should be used when existing accessToken has expired its validity.

Generate Access Token using Curl.

> curl trusted:secret@localhost:8081/oauth/token -d grant_type=password -d username=user -d password=password

Sample AccessToken Response
```json
{
"access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiIyY2UzNTM2MC1lZjhlLTRmNjktYTh
"expires_in": 2627999,
"jti": "5b42ca29-8b61-4a3a-8502-53c21e85a117",
"refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiIyY2UzNTM2MC1lZjhlLTRmNjktYT
"scope": "read",
"token_type": "bearer",
"uid": "2ce35360-ef8e-4f69-a8d7-b5d1aec78759"
}
```


How to use a RefreshToken to request a new AccessToken?
-------
RefreshToken is used to create a new AccessToken once existing AccessToken is expired. The client requesting this operation must present its own clientId and clientSecret to oauth server to perform this operation.

Using curl to generate a new AccessToken using RefreshToken

Curl can be used at command line to generate the new AccessToken by presenting RefreshToken and client credentials to OAuth Server.

Request.
> curl <client-id>:<client-secret>@localhost:9999/uaa/oauth/token -d grant_type=refresh_token -d refresh_token=$REFRESH_TOKEN

Response.
```json
{
"access_token":"$ACCESS_TOKEN",
"token_type":"bearer",
"refresh_token":"$REFRESH_TOKEN",
"expires_in":86399,
"scope":"openid",
"userId":1,
"authorities":[ROLE_USER],
"jti":"cd4ec2ad-ac88-4dd7-b937-18dd22e9410e"
}
```

**Using RestTemplate to generate a new AccessToken using RefreshToken**

Android Apps can use RestTemplate to renew their accessToken. The returned accessToken can be saved for subsequent calls to protected resources.


```java
public OAuthTokenDto renewToken(final OAuthTokenDto existingToken) {
   String requestUrl = authBaseUrl + "oauth/token";
   MultiValueMap<String, String> map = new LinkedMultiValueMap<>();
   map.add("grant_type", "refresh_token");
   map.add("refresh_token", existingToken.getRefresh_token());
   map.add("scope", "read");
   HttpAuthentication authHeader = new HttpBasicAuthentication(CLIENT_ID, CLIENT_SECRET);
   HttpHeaders headers = new HttpHeaders();
   headers.setContentType(MediaType.APPLICATION_FORM_URLENCODED);
   headers.setAccept(Collections.singletonList(MediaType.APPLICATION_JSON));
   headers.setAuthorization(authHeader);
   HttpEntity<MultiValueMap<String, String>> entity = new HttpEntity<>(map, headers);
   RestTemplate restTemplate = new RestTemplate();
   final ResponseEntity<OAuthTokenDto> responseEntity =
        restTemplate.exchange(requestUrl, HttpMethod.POST, entity, OAuthTokenDto.class);
   return responseEntity.getBody();
}
```



How to call the protected resource using AccessToken?
-------
Protected resources from microservices can be accessed by passing Authorization Bearer token in request headers, using curl the request looks like below - 

> curl -H "Authorization: Bearer <AccessToken>" -v localhost:9090/user/info

JSON Response.
```json
{
"key": "value"
...
}

```

The same call can be made using RestTemplate, Retrofit, FeignClient, RestAssured api or POSTMAN interface.

**Calling Protected Resource using RestTemplate**

Create HTTP headers that populates Bearer Token, like shown below:

```java
public static HttpHeaders createHeaders() {
   final String access_token = $ACCESS_TOKEN;
   return new HttpHeaders() {
         {
            set("Authorization", "Bearer " + access_token);
         }
      };
      }
```

ACCESS_TOKEN can be stored on Android Device SharedPreference and pciked up in this method.

And then use the above created Headers in RestTemplate, like shown below-

**RestTemplate Call**.
```java
HttpEntity<Object> httpEntity = new HttpEntity<>(ApplicationContext.createHeaders());
ResponseEntity<String> responseEntity = restTemplate.exchange(url, HttpMethod.GET, httpEntity, String.class, uriVariables);
```

Can a refreshToken be never expiring? How to make refreshToken life long valid?
-------
We can set the validity for refreshToken to a negative value, zero or Integer.MAX_VALUE to make it never expiring.

```java
@Bean
public AuthorizationServerTokenServices tokenServices() throws Exception {
        DefaultTokenServices tokenServices = new DefaultTokenServices();
        tokenServices.setTokenStore(tokenStore);
        tokenServices.setSupportRefreshToken(true);
        tokenServices.setClientDetailsService(clientDetailsService);
        tokenServices.setRefreshTokenValiditySeconds(Integer.MAX_VALUE);
        return tokenServices;
        }
```
**Caution**

It is not a good idea to make refreshToken never expiring due to security concerns. A better approach in this case could be to set reuseRefreshTokens(false) to create a new RefreshToken everytime a new AccessToken is created. This way, client credentials would still be required to generate the new refreshToken.

AWS Cognito only allows 3650 days as the maximum interval for refresh token expiry. The default expiry is set to 30 days, though. AccessToken expiry is set to a fixed value of 1 hour which can not be changed.

Generate AccessToken for Client Credentials.
-------
Client Credentials can be used by clients (client applications or microservices, that are not human) for inter service communication.

Request using Curl.

> curl service-account-1:service-account-1-secret@localhost:8080/auth/oauth/token -d grant_type=cli

Token Response.

```json
{
"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzY29wZSI6WyJyZWFkIiwid3JpdGUiXSwiZXh
"expires_in": 43199,
"jti": "da93ce67-a97a-4a66-8778-417518c4aa08",
"scope": "read write",
"token_type": "bearer"
}
```
Now this token can be used for making protected endpoint call on resource server.


**Using AccessToken to access protected resource.**

> curl -H "Authorization: Bearer $TOKEN" -v http://localhost:8082/api

Where `$TOKEN` is the Access Token.

Why there is no RefreshToken support in Oauth2 Client Credentials workflow?
-------

First of all we need to understand why RefreshToken grant type is provided in oauth2 specs. In Resource Owner Credentials workflow, a client (usually a mobile app) accesses protected resources on behalf of end user (resource owner). Now since client does not have access to user’s credentials, refresh token helps getting a new access token by its own, by presenting client’s credentials along with the refresh token to oauth server. This way an end user can be kept logged in to the mobile app for a much longer duration.

On the other hand, Client Credentials workflow is always meant for machine to machine communication that is not on behalf of resource owner (human). Since client will always have access to its own credentials, so it can always present the credentials to oauth server and obtain a new access token after expiry.


Security in inter-service communication
-------

There could be two usecases for inter service communication -
1. Calling one service from another on behalf of user request.
2. Using Service Client for internal service to service communication.
   
**Token Relay**

In first case, we shall propagate the security context of user from one service to another.

We can configure OAuth2RestTemplate to relay user token from service to service.

This approach shall be used when a client (often a microservice) want to relay token to downstream service in order to access a protected resource on behalf of user.

A Load Balanced OAuth2RestTemplate that Relays Token.

```java
@LoadBalanced
@Bean
@Autowired
public OAuth2RestTemplate loadBalancedOauth2RestTemplate(OAuth2ClientContext oauth2ClientCont
    return new OAuth2RestTemplate(details, oauth2ClientContext);
}
```

Using OAuth2RestTemplate to make remote protected calls in another microservice..

```java
@Service
public class RemoteMicroService {
   @Autowired
   private OAuth2RestTemplate oAuth2RestTemplate;
    //Use this oAuth2RestTemplate to make protected remote calls with user's token relay.
```


**Client Credentials**

In second case, we shall use Client Credentials issued by OAuth2 workflow for securing service to service communication. Here user’s security context is not propogated to the downstream server, instead the client’s credentials are used to secure the communication.

<img src="./images-ms/Client Crendtials Sequence Diagram.png" width="800" border="2" />

This approach shall mostly be used for scheduled jobs where we are not making remote service calls on behalf of end user.

Creating a RestTemplate based on Client Credentials.

```java
@Configuration
public class RestTemplateConfig {
   //Client Credentials based oAuth2 RestTemplate for Service Client Inter Microservice Communic
   @Bean(name = "oauthRestTemplate")
   public RestTemplate oAuthRestTemplate() {
      ClientCredentialsResourceDetails resourceDetails = new ClientCredentialsResourceDetails()
      resourceDetails.setId("<Id>");
      resourceDetails.setClientId("<clientId>");
      resourceDetails.setClientSecret("<clientsecret>");
// resourceDetails.setAccessTokenUri("<BaseUrl>/uaa/oauth/token");
      resourceDetails.setScope(Collections.singletonList("openid"));
      return new OAuth2RestTemplate(resourceDetails, new DefaultOAuth2ClientContext());
   }
```
This restTemplate can now be used for internal service communication, for example -
```java
@Service
public class ProfileImageSyncService {
   private static final Logger logger = LoggerFactory.getLogger(ProfileImageSyncService.class);
   @Autowired
   @Qualifier("oauthRestTemplate")
   private RestTemplate restTemplate;
   public void doSomeRemoteWork() {
      ResponseEntity<String> responseEntity = restTemplate.exchange(targetUrl, HttpMethod.GET, nu
      ...Do something withr response.
      ...
    }

```

`Warning`
We shall never use ResourceOwnerPasswordCredentials for internal service communication, thats a anti-pattern. Client Credentials should always be preferred when one service wants to talk to another service based on some scheduled job (not on behalf of user request), otherwise user’s security token should be relayed to the next service if request is initiated by end user.


