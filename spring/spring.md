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

Constructor Vs Setter injection 
-----------------------
The differences are:
- Partial dependency is not possible with Constructor based injection, but it is possible with Setter based injection. Suppose there are 4 properties in a class and the class has setter methods and a constructor with 4 parameters. In this case, if you want to inject only one/two property, then it is only possible with setter methods (unless you can define a new parametrized constructor with the needed properties)
- Cyclic dependency is also not possible with Constructor based injection. Suppose class A has dependency on class B and class B has dependency on class A and we are using constructor based injection, then when Spring tries to create object of class A, it sees that it needs class B object, then it tries to resolve that dependency first. But when it tries to create object of class B, it finds that it needs class A object, which is still under construction. Here Spring recognizes that a circular reference may have occurred and you will get an error in this case. This problem can easily be solved by using Setter based injection because dependencies are not injected at the object creation time
- While using Constructor injection, you will have to remember the order of parameters in a constructor when the number of constructor parameters increases. This is not the case with Setter injection
- Constructor injection helps in creating immutable objects, because a bean object is created using constructor and once the object is created, its dependencies cannot be altered anymore. Whereas with Setter injection, it’s possible to inject dependency after object creation which leads to mutable objects.

Use constructor-based injection, when you want your class to not even be instantiated if the class dependencies are not resolved because Spring container will ensure that all the required dependencies are passed to the constructor.


BeanFactory and ApplicationContext
-----------------------
The differences are:

- BeanFactory is the most basic version of IOC containers which should be preferred when memory consumption is critical whereas ApplicationContext extends BeanFactory, so you get all the benefits of BeanFactory plus some advanced features for enterprise applications
- BeanFactory instantiates beans on-demand i.e. when the method getBean(beanName) is called, it is also called Lazy initializer whereas ApplicationContext instantiates beans at the time of creating the container where bean scope is Singleton, so it is an Eager initializer
- BeanFactory only supports 2 bean scopes, singleton and prototype whereas ApplicationContext supports all bean scopes
- ApplicationContext automatically registers BeanFactoryPostProcessor and BeanPostProcessor at startup, whereas BeanFactory does not register these interfaces automatically
- Annotation based dependency injection is not supported by BeanFactory whereas ApplicationContext supports it
- If you are using plain BeanFactory, features like transactions and AOP will not take effect (not without some extra steps), even if nothing is wrong with the configuration whereas in ApplicationContext, it will work
- ApplicationContext provides additional features like MessageSource access (i18n or Internationalization) and Event Publication 

Use an ApplicationContext unless you have a really good reason for not doing so.

Spring Bean life-cycle
-----------------------
Spring beans are java classes that are managed by Spring container and the bean life-cycle is also managed by Spring container.

The bean life-cycle has below steps:
- Bean instantiated by container
- Required dependencies of this bean are injected by container
- Custom Post initialization code to be executed (if required)
- Bean methods are used
- Custom Pre destruction code to be executed (if required)

When you want to execute some custom code that should be executed before the bean is in usable state, you can specify an init() method and if some custom code needs to be executed before the bean is destroyed, then a destroy() method can be specified.
There are various ways to define these init() and destroy() method for a bean:

By using xml file,
<bean> tag has 2 attributes that can be used to specify its init  and destroy methods,

You can give any name to your initialization and destroy methods, and here is our Test class

```java
package com.demo;
public Class Test{
    public void init() throws Exception{
        System.out.prinln("Init Method");
    }
    public void destroy() throws Exception{
        System.out.prinln("Destroy Method");
    }
}
```

By implementing InitializingBean and DisposableBean interfaces

InitializingBean interface has afterPropertiesSet() method which can be used to execute some initialization task for a bean and DisposableBean interface has a destroy() method which can be used to execute some cleanup task.

Here is our Test class,

```java
package com.demo;


```

Spring Bean Scopes
------------------
Spring framework supports 5 scopes: 
- **singleton** – only one bean instance per Spring IOC container
- **prototype** – it produces a new instance each and every time a bean is requested
- **request** – a single instance will be created and made available during complete life-cycle of an HTTP request
- **session** – a single instance will be created and made available during complete life-cycle of an HTTP session
- **global session** – a single instance will be created during the life-cycle of a ServletContext

`@Scope` annotation or scope attribute of bean tag can be used to define bean scopes in Spring. 

Default scope of a bean is `Singleton` that means only one instance per context. 

What happens when we inject a prototype scope bean in a singleton scope bean?
------------------
When you define a bean scope to be singleton, that means only one instance will be created and whenever we request for that bean, that same instance will be returned by the Spring container, however, a prototype scoped bean returns a new instance every time it is requested.

Spring framework gets only one chance to inject the dependencies, so if you try to inject a prototyped scoped bean inside a singleton scoped bean, Spring will instantiate the singleton bean and will inject one instance of prototyped scoped bean. This one instance of prototyped scoped bean is the only instance that is ever supplied to the singleton scoped bean.

So here, whenever the singleton bean is requested, `you will get the same instance of prototyped scoped bean`.

How to inject a prototype scope bean in a singleton scope bean?
------------------
We have discussed in the previous question that when a prototyped scoped bean is injected in a singleton scoped bean, then on each request of singleton bean, we will get the same instance of prototype scoped bean, but there are certain ways where we can get a new instance of prototyped scoped bean also.

The solutions are:
- Injecting an ApplicationContext in Singleton bean and then getting the new instance of prototyped scoped bean from this ApplicationContext
- Lookup method injection using @Lookup
- Using scoped proxy

**Injecting ApplicationContext:**

To inject the ApplicationContext in Singleton bean, we can either use @Autowired annotation or we can implement ApplicationContextAware interface,

```java
package com.demo;

import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContextAware;
import org.springframework.context.ApplicationContext;
import org.springframework.sterotype.Component;

@Component
public class SingletonBean implements ApplicationContextAware{
    
    private ApplicationContext applicationContext;
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException{
        this.applicationContext=applicationContext;
    }

    public PrototypeBeann getProtoTypeBean(){
        return. applicationContext.getBean(PrototypeBean.class);
    }
}

```

Here, whenever the getPrototypeBean() method is called, it will return a new instance of PrototypeBean.
But this approach contradicts with Spring IOC (Inversion of Control), as we are requesting the dependencies directly from the container.



**Lookup Method Injection using @Lookup:**

```java
package com.demo;

import org.springframework.beans.factory.annotations.Lookup;
import org.springframework.sterotype.Component;

@Component
public class SingletonBean {
    @Lookup
    public PrototypeBeann getProtoTypeBean(){
        return null;
    }
}

```

Here, Spring will dynamically overrides getPrototypeBean() method annotated with @Lookup and it will look up the bean which is the return type of this method. Spring uses CGLIB library to do this.

**Using Scoped Proxy**

```java
package com.demo;

import org.springframework.beans.factory.ConfigurableBeanFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Scope;
import org.springframework.context.annotation.ScopedProxyMode;
import org.springframework.sterotype.Component;

import java.beans.BeanProperty;

@Component
public class SingletonBean {

    private ApplicationContext applicationContext;

    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        this.applicationContext = applicationContext;
    }

    @Bean
    @Scope(value=ConfigurableBeanFactory.ScopedProxyMode,
    proxyMode=ScopedProxyMode.TARGET_CLASS)
    public PrototypeBean getProtoTypeBean() {
        return new PrototypeBean();
    }
}

```

Spring uses CGLIB to create the proxy object and the proxy object delegates method calls to the real object. In the above example, we are using ScopedProxyMode.TARGET_CLASS which causes an AOP proxy to be injected at the target injection point. The default Proxy mode is ScopedProxyMode.NO .

To avoid CGLIB usage, configure the proxy mode with ScopedProxyMode.INTERFACES and it will use JDK dynamic proxy. 

Stereotype Annotations
----------------------

`@Component`, `@Controller`, `@Service` and `@Repository` annotations are called stereotype annotations and they are present in org.springframework.stereotype package.

@Component: it is a general purpose stereotype annotation which indicates that the class annotated with it, is a spring managed component.

@Controller, @Service and @Repository are special types of @Component, these 3 themselves are annotated with @Component,

```java
package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Indexed
public @interface Component {
    String value() default "";
} 
```

```java

package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Controller {
    @AliasFor(
            annotation = Component.class
    )
    String value() default "";
}
```




```java
package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Service {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

```java

package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Repository {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```


So, the classes annotated with these annotations gets picked up in Component scanning and they are managed by Spring.

- **@Controller:** the classes annotated with `@Controller` will act as Spring MVC controllers. DispatcherServlet looks for `@RequestMapping` in classes that are annotated with `@Controller`. That means you cannot replace `@Controller` with `@Component`, if you just replace it with `@Component` then yes it will be managed by Spring but it will not be able to handle the requests.
(Note: if a class is registered with Spring using `@Component`,  then @RequestMapping annotations within class can be picked up, if the class itself is annotated with @RequestMapping)

- **@Service:** The service layer classes that contain the business logic should be annotated with `@Service`. Apart from the fact that it is used to indicate that the class contains business logic, there is no special meaning to this annotation, however it is possible that Spring may add some additional feature to `@Service` in future, so it is always good idea to follow the convention.

- **@Repository:** The classes annotated with this annotation defines data repositories. It is used in DAO layer classes. @Repository has one special feature that it catches platform specific exceptions and re-throw them as one of the Spring’s unified unchecked exception i.e. `DataAccessException` .


@Controller vs @RestController annotation
-----------------------
The differences are:

- `@Controller` annotation is used to mark a class as Spring MVC controller where the response is a view name which will display the Model object prepared by controller, whereas @RestController annotation is a specialization of @Controller and it is used in RESTful web services where the response is usually JSON/XML.
- `@RestController` is made up of 2 annotations, @Controller and @ResponseBody. @ResponseBody annotation is used to attach the generated output directly into the body of http response.
- `@Controller` can be used with @ResponseBody which will have same effect as @RestController. @ResponseBody annotation can be used at the class level or at the individual methods also. When it is used at the method level, Spring will use HTTP Message Converters to convert the return value to HTTP response body (serialize the object to response body).

@Qualifier annotation
-----------------------
Let’s consider an example to understand @Qualifier annotation better. Suppose we have an interface called Shape and there are 2 classes Rectangle and Circle that are implementing this interface. We are autowiring our Shape interface in our controller class using @Autowired, now here a conflict will happen, because there are 2 beans of the same type.


```java
public interface Shape{

}

@Service 
public class Rectangle implements Shape{


}

@Service 
public class Circle implements Shape{

}


@RestController
public class ShapeCOntroller{


@Autowired
Shape shape;

}
```

When you try to start your application, you will get

```log
Could not autowire. There is more than one bean of 'Shape' type.
Beans:
circle (Circle.java) rectangle  (Rectangle.java) 
```

Now, to resolve this you can give names to your Rectangle and Circle class, like: 


```java
public interface Shape{

}

@Service("rectangle")
public class Rectangle implements Shape{


}

@Service("circle") 
public class Circle implements Shape{

}
```

And you will use @Qualifier annotation to specify which bean should be autowired, like:
```java
@RestController
public class ShapeCOntroller{
    @Autowired
    @Qualifier("circle")
    Shape shape;
}
```

Now, Spring will not get confused as to what bean it has to autowire.
NOTE , you can also use @Qualifier annotation to give names to your Rectangle and Circle classes, like
```java
@RestController
public class ShapeCOntroller{
    @Autowired
    @Qualifier("rectangle")
    Shape shape;
}
```


@Transactional annotation
 -----------------------

Spring provides Declarative Transaction Management via `@Transactional` annotation. When a method is applied with `@Transactional`, then it will execute inside a database transaction. '@Transactional' annotation can be applied at the class level also, in that case, all methods of that class will be executed inside a database transaction.

**How @Transactional works:**

When '@Transactional' annotation is detected by Spring, then it creates a proxy object around the actual bean object. So, whenever the method annotated with '@Transactional' is called, the request first comes to the proxy object and this proxy object invokes the same method on the target bean. These proxy objects can be supplied with interceptors. Spring creates a TransactionInterceptor and passes it to the generated proxy object. So, when the '@Transactional' annotated method is called, it gets called on the proxy object first, which in turn invokes the TransactionInterceptor that begins a transaction. Then the proxy object calls the actual method of the target bean. When the method finishes, the TransactionInterceptor commits/rollbacks the transaction.

One thing to remember here is that the Spring wraps the bean in the proxy, the bean has no knowledge of it. So, only the external calls go through the proxy. As for the internal calls ('@Transactional' method calling the same bean method), they are called using ‘this’.
Using '@Transactional' annotation, the transaction’s propagation and isolation can be set directly, like: 

```java

 @Transactional(propogation = Propogationn.REQUIRES_NEW,
        isolation = Isolation.READ_UNCOMMITTES
        rollbackFor = Exception.class)
 public String process(){
            return "Success";
        }
 
```
Also, you can specify a ‘rollbackFor’ attribute and specify which exception types must cause a transaction rollback (a transaction with Runtime exceptions and errors are by default rolled back).
If your process() method is calling another bean method, then you can also annotate that method with '@Transactional' and set the propagation level to decide whether this method should execute in the same transaction or it requires a new transaction.

@ControllerAdvice annotation
-----------------------
`@ControllerAdvice` annotation is used to intercept and handle the exceptions thrown by the controllers across the application, so it is a global exception handler. You can also specify @ControllerAdvice for a specific package,

```java
@ControllerAdvice(basePackage = com.demo.controller")
public class Test{

}
```

Or a specific controller,
```java
@ControllerAdvice(assignableTypes=  = DemoController.class)
public class Test{

}
```

Or even a specific annotation,
```java
@ControllerAdvice(annotations=  = RestController.class)
public class Test{

}
```
`@ExceptionHandler` annotation is used to handle specific exceptions thrown by controllers, like,
```java
@ControllerAdvice
public class Test{
    ExceptioHandler(SQLException.class)
    public String handleSQLException(){
        return null;
    }
    
    ExceptioHandler(UserNotFoundException.class)
    public String handleUserNotFoundException(){
        return null;
    }
}
```

Here, we have defined a global exception handler using `@ControllerAdvice`. If a SQLException gets thrown from a controller, then `handleSQLException()` method will be called. In this method, you can customize the exception and send a particular error page/error code. Also, custom exceptions can be handled.

If you don’t want to create a global exception handler, then you can also define some `@ExceptionHandler` methods in a particular controller itself.



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