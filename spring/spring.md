Spring
=================

PUT, POST, GET, DELETE and PATCH IN HTTP
------------------

POST is always for creating a resource ( does not matter if it was duplicated )
PUT is for checking if resource is exists then update , else create new resource
PATCH is always for update a resource


Dependency Injection
-------------------

Dependency Injection is the most important feature of Spring framework. Dependency Injection is a design pattern where the dependencies of a class are injected from outside, like from an xml file. It ensures loose-coupling between classes.

In a Spring MVC application, the controller class has dependency of service layer classes and the service layer classes have dependencies of DAO layer classes.

Suppose class A is dependent on class B. In normal coding, you will create an object of class B using ‘new’ keyword and call the required method of class B. However, what if you can tell someone to pass the object of class B in class A? Dependency injection does this. You can tell Spring, that class A needs class B object and Spring will create the instance of class B and provide it in class A.

In this example, we can see that we are passing the control of objects to Spring framework, this is called Inversion of Control (IOC) and Dependency injection is one of the principles that enforce IOC.


Types of Dependency Injection
-----------------------------
Spring framework provides 2 ways to inject dependencies:
- By Constructor
- By Setter method

**Constructor-based DI** :
-----------------------------

when the required dependencies are provided as arguments to the constructor, then it is known as constructor-based dependency injection, see the examples below:

_Using XML based configuration:_
Injecting a dependency is done through the bean-configuration file, for this <constructor-arg> xml tag is used:

```xml
 <bean id="classB" class="com.demo.B" />

<bean id="classA" class="com.demo.A">
         <constructor-arg ref="classB" /> 
</bean>
```

In case of more than 1 dependency, the order sequence of constructor arguments should be followed to inject the dependencies.
Java Class A:
```java
package com.demo;
public Class A{
    B b;
    A(B b){
        this.b=b;
        }
}
```
Java Class B:

```java
package com.demo;
public Class B{
   
}
```

**Using Java Based Configuration:**

When using Java based configuration, the constructor needs to be annotated with `@Autowired` annotation to inject the dependencies,

Classes A and B will be annotated with `@Component` (or any other stereotype annotation), so that they will be managed by Spring.

```java
package com.demo;
package org.springframework.beans.factory.annotation.Autowired;
package  org.springframework.stereotype.Component;

@Component
public Class A{
    B b;
    @Autowired
    A(B b){
            this.b=b;
    }
}
```
Java class B:

```java
package com.demo;
package org.springframework.stereotype.Component;

@Component
public Class B{

}
```

Before Spring version 4.3, `@Autowired` annotation was needed for constructor dependency injection, however, in newer Spring versions, @Autowired is optional, if the class has only one constructor.
But, if the class has multiple constructors, we need to explicitly

But, if the class has multiple constructors, we need to explicitly add ``@Autowired`` to one of the constructors so that Spring knows which constructor to use for injecting the dependencies.


Setter-method injection: 
------------------------

in this, the required dependencies are provided as the field parameters to the class and the values are set using setter methods of those properties. See the examples below.

**Using XML based configuration:**
Injecting a dependency is done through the bean configuration file and <property> xml tag is used where ‘name’ attribute defines the name of the field of java class. 


```xml
 <bean id="classB" class="com.demo.B" />

<bean id="classA" class="com.demo.A">
<property name="b">
         <constructor-arg ref="classB" />
</property>
</bean>
```



Java Class A:
```java
package com.demo;
public Class A{
    B b;
    public void setB(B b){
        this.b=b;
        }
}
```
Java Class B:

```java
package com.demo;
public Class B{

        }
```
**Using Java based configuration:**

The setter method needs to be annotated with `@Autowired` annotation. 

```java
package com.demo;
package org.springframework.beans.factory.annotation.Autowired;
package  org.springframework.stereotype.Component;

@Component
public Class A{
    B b;
    @Autowired
    public void setB(B b){
            this.b=b;
    }
}
```
Java class B:

```java
package com.demo;
package org.springframework.stereotype.Component;

@Component
public Class B{

}
```

There is also a Field injection, where Spring injects the required dependencies directly into the fields when those fields are annotated with `@Autowired` annotation.


Spring Boot Security using OAuth2 with JWT
-----------------------

OAuth2 is an authorization framework superseding it first version OAuth, created back in 2006. It defines the authorization flows between clients and one or more HTTP services in order to gain access to protected resources.

The main goal of the OAuth2 framework is to provide a simple flow of authorization that can be implemented on the web application, mobile phones, desktop application, and even on the devices used in our living rooms.

OAuth2 defines the following server-side roles:

- **Resource Owner**: The service responsible for controlling resources’ access
- **Resource Server**: The service who actually supplies the resources
- **Authorization Server**: The service handling authorization process acting as a middleman between client and resource owner
- **JSON Web Token, or JWT**, is a specification for the representation of claims to be transferred between two parties. The claims are encoded as a JSON object used as the payload of an encrypted structure, enabling the claims to be digitally signed or encrypted.

OAuth2 Terminology
------------------
- **Resource Owner** The user who authorizes an application to access his account. The access is limited to the `scope`.
- **Resource Server:** A server that handles authenticated requests after the `client` has obtained an `access token`.
- **Client** An application that access protected resources on behalf of the resource owner.
- **Authorization Server** A server which issues access tokens after successfully authenticating a `client` and `resource owner`, and authorizing the request.
- **Access Token** A unique token used to access protected resources
- **Scope** A Permission
- **JWT** JSON Web Token is a method for representing claims securely between two parties.
- **Grant type** A `grant` is a method of acquiring an access token. 

Json Web Token(JWT)
------------------

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.a stateless authentication mechanism as the user state is never saved in server memory.A JWT token consists of 3 parts seperated with a dot(.) i.e. Header.payload.signature

Header has 2 parts type of token and hashing algorithm used.The JSON structure comprising these two keys are Base64Encoded.

```json
{
"alg": "HS256",
"typ": "JWT"
}
```
Payload contains the claims.Primarily, there are three types of claims: reserved, public, and private claims. Reserved claims are predefined claims such as iss (issuer), exp (expiration time), sub (subject), aud (audience).In private claims, we can create some custom claims such as subject, role, and others.

```json
{
"sub": "Alex123",
"scopes": [
{
"authority": "ROLE_ADMIN"
}
],
"iss": "http://devglan.com",
"iat": 1508607322,
"exp": 1508625322
}
```
Signature ensures that the token is not changed on the way.For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```log
HMACSHA256(
base64UrlEncode(header) + "." +
base64UrlEncode(payload),
secret)
```

sample JWT token
```log
eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJBbGV4MTIzIiwic2N.v9A80eU1VDo2Mm9UqN2FyEpyT79IUmhg
```

_Spring Boot Rest Authentication with JWT Token Flow_
------------------
- Customers sign in by submitting their credentials to the provider.
- Upon successful authentication, it generates JWT containing user details and privileges for accessing the services and sets the JWT expiry date in payload.
- The server signs and encrypts the JWT if necessary and sends it to the client as a response with credentials to the initial request.
- Based on the expiration set by the server, the customer/client stores the JWT for a restricted or infinite amount of time.
- The client sends this JWT token in the header for all subsequent requests.
- The client authenticates the user with this token. So we don't need the client to send the user name and password to the server during each authentication process, but only once the server sends the client a JWT.



For more information:

1. [Using Spring Boot for OAuth2 and JWT REST Protection](https://www.toptal.com/spring/spring-boot-oauth2-jwt-rest-protection)
2. [Spring Boot Security + JWT (JSON Web Token) Authentication Example](https://www.techgeeknext.com/spring/spring-boot-security-token-authentication-jwt)
3. [Spring Boot Security using OAuth2 with JWT](https://www.pixeltrice.com/spring-boot-security-using-oauth2-with-jwt/)
4. [What is the difference between PUT, POST and PATCH? [closed]](https://stackoverflow.com/questions/31089221/what-is-the-difference-between-put-post-and-patch#:~:text=POST%20is%20always%20for%20creating,always%20for%20update%20a%20resource)