Spring Boot
==========


Spring Boot is an opinionated addition to the Spring platform, focused on convention over configuration — highly useful for getting started with minimum effort and creating standalone, production-grade applications.

Spring Boot is basically an extension of the Spring framework which eliminated the boilerplate configurations required for setting up a Spring application.

Spring Boot is an opinionated framework that helps developers build Spring-based applications quickly and easily. The main goal of Spring Boot is to quickly create Spring-based applications without requiring developers to write the same boilerplate configuration again and again.

Spring Boot Primary Goals
--------------------
- Provide a radically faster and widely accessible getting-started experience for all Spring development.
- Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
- Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
- Absolutely no code generation and no requirement for XML configuration.

Key Spring Boot features
--------------------
- Spring Boot starters
- Spring Boot autoconfiguration
- Elegant configuration management
- Spring Boot actuator
- Easy-to-use embedded servlet container support

Spring Boot Starters
--------------------
Spring Boot offers many starter modules to get started quickly with many of the commonly used technologies, like SpringMVC, JPA, MongoDB, Spring Batch, SpringSecurity, Solr, ElasticSearch, etc. These starters are pre-configured with the most commonly used library dependencies so you don’t have to search for the compatible library versions and configure them manually.

`For example,` the spring-boot-starter-data-jpa starter module includes all the dependencies required to use Spring Data JPA, along with Hibernate library dependencies, as Hibernate is the most commonly used JPA implementation.

One more example, when we add the `spring-boot-starter-web` dependency, it will by default pull all the commonly used libraries while developing Spring MVC applications, such as spring-webmvc, jackson-json, validation-api, and tomcat.

Not only does the `spring-boot-starter-web` add all these libraries but it also configures the commonly registered beans like DispatcherServlet, ResourceHandlers, MessageSource, etc. with sensible defaults.

Spring Boot Autoconfiguration
--------------------
Spring Boot addresses the problem that Spring applications need complex configuration by eliminating the need to manually set up the boilerplate configuration.
Spring Boot takes an opinionated view of the application and configures various components automatically, by registering beans based on various criteria. The criteria can be:

- Availability of a particular class in a classpath
- Presence or absence of a Spring bean
- Presence of a system property
- An absence of a configuration file

`For example,` if you have the spring-webmvc dependency in your classpath, Spring Boot assumes you are trying to build a SpringMVC-based web application and automatically tries to register DispatcherServlet if it is not already registered. If you have any embedded database drivers in the classpath, such as H2 or HSQL, and if you haven’t configured a DataSource bean explicitly, then Spring Boot will automatically register a DataSource bean using in-memory database settings.

Easy-to-Use Embedded Servlet Container Support
--------------------
Traditionally, while building web applications, you need to create WAR type modules and then deploy them on external servers like Tomcat, WildFly, etc. But by using Spring Boot, you can create a JAR type module and embed the servlet container in the application very easily so that the application will be a self-contained deployment unit.

Also, during development, you can easily run the Spring Boot JAR type module as a Java application from the IDE or from the command-line using a build tool like Maven or Gradle.


Spring Boot Annotations
--------------------

@SpringBootApplication
--------------------

We use this annotation to mark the main class of a Spring Boot application.

`@SpringBootApplication` encapsulates `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan` annotations with their default attributes.

```java
@SpringBootApplication
class VehicleFactoryApplication {

    public static void main(String[] args) {
        SpringApplication.run(VehicleFactoryApplication.class, args);
    }
}
```

@EnableAutoConfiguration
--------------------
@EnableAutoConfiguration, as its name says, enables auto-configuration. It means that Spring Boot looks for auto-configuration beans on its classpath and automatically applies them.

Note, that we have to use this annotation with @Configuration:
```java
@Configuration
@EnableAutoConfiguration
class MyConfig {
    
}
```

@ConditionalOnClass and @ConditionalOnMissingClass
--------------------
Using these conditions, Spring will only use the marked auto-configuration bean if the class in the annotation's argument is present/absent:
```java
@Configuration
@ConditionalOnClass(DataSource.class)
class MySQLAutoconfiguration {
    //...
}
```

@ConditionalOnBean and @ConditionalOnMissingBean
--------------------
We can use these annotations when we want to define conditions based on the presence or absence of a specific bean:
```java
@Bean
@ConditionalOnBean(name = "dataSource")
LocalContainerEntityManagerFactoryBean entityManagerFactory() {
        // ...
}
```


@ConditionalOnProperty
--------------------
With this annotation, we can make conditions on the values of properties:

```java
@Bean
@ConditionalOnProperty(
        name = "usemysql",
        havingValue = "local"
)
DataSource dataSource() {
        // ...
}
```

@ConditionalOnResource
--------------------
We can make Spring to use a definition only when a specific resource is present:
```java
@ConditionalOnResource(resources = "classpath:mysql.properties")
Properties additionalProperties() {
        // ...
}
```

@ConditionalOnWebApplication and @ConditionalOnNotWebApplication
--------------------
With these annotations, we can create conditions based on if the current application is or isn't a web application:
```java
@ConditionalOnWebApplication
HealthCheckController healthCheckController() {
        // ...
}
```

@ConditionalExpression
--------------------
We can use this annotation in more complex situations. Spring will use the marked definition when the SpEL expression is evaluated to true:
```java
@Bean
@ConditionalOnExpression("${usemysql} && ${mysqlserver == 'local'}")
DataSource dataSource() {
        // ...
}
```

@Conditional
--------------------
we can create a class evaluating the custom condition. We tell Spring to use this custom condition with @Conditional:

```java
@Conditional(HibernateCondition.class)
Properties additionalProperties() {
        //...
}
```


Spring Boot Actuator
--------------------

- Actuator brings production-ready features to our application.
- Monitoring our app, gathering metrics, understanding traffic, or the state of our database become trivial with this dependency.
- The main benefit of this library is that we can get production-grade tools without having to actually implement these features ourselves.
- Actuator is mainly used to expose operational information about the running application — health, metrics, info, dump, env, etc. It uses HTTP endpoints or JMX beans to enable us to interact with it.
- Once this dependency is on the classpath, several endpoints are available for us out of the box. As with most Spring modules, we can easily configure or extend it in many ways.


spring-boot-actuator maven dependency
--------------------

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Predefined Endpoints
--------------------

- `/auditevents` lists security audit-related events such as user login/logout. Also, we can filter by principal or type among other fields.
- `/beans` returns all available beans in our BeanFactory. Unlike /auditevents, it doesn't support filtering.
- `/conditions`, formerly known as /autoconfig, builds a report of conditions around autoconfiguration.
- `/configprops` allows us to fetch all @ConfigurationProperties beans.
- `/env` returns the current environment properties. Additionally, we can retrieve single properties.
- `/flyway` provides details about our Flyway database migrations.
- `/health` summarizes the health status of our application.
- `/heapdump` builds and returns a heap dump from the JVM used by our application.
- `/info` returns general information. It might be custom data, build information or details about the latest commit.
- `/liquibase` behaves like /flyway but for Liquibase.
- `/logfile` returns ordinary application logs.
- `/loggers` enables us to query and modify the logging level of our application.
- `/metrics` details metrics of our application. This might include generic metrics as well as custom ones.
- `/prometheus` returns metrics like the previous one, but formatted to work with a Prometheus server.
- `/scheduledtasks` provides details about every scheduled task within our application.
- `/sessions` lists HTTP sessions given we are using Spring Session.
- `/shutdown` performs a graceful shutdown of the application.
- `/threaddump` dumps the thread information of the underlying JVM.


/info Endpoint
--------------------
We can also customize the data shown by the /info endpoint:
```properties
info.app.name=Spring Sample Application
info.app.description=This is my first spring boot application
info.app.version=1.0.0
```

And the sample output:

```json
{
    "app" : {
        "version" : "1.0.0",
        "description" : "This is my first spring boot application",
        "name" : "Spring Sample Application"
    }
}
```

/metrics Endpoint
--------------------
The metrics endpoint publishes information about OS and JVM as well as application-level metrics. Once enabled, we get information such as memory, heap, processors, threads, classes loaded, classes unloaded, and thread pools along with some HTTP metrics as well.

Here's what the output of this endpoint looks like out of the box:
```json
{
    "mem" : 193024,
    "mem.free" : 87693,
    "processors" : 4,
    "instance.uptime" : 305027,
    "uptime" : 307077,
    "systemload.average" : 0.11,
    "heap.committed" : 193024,
    "heap.init" : 124928,
    "heap.used" : 105330,
    "heap" : 1764352,
    "threads.peak" : 22,
    "threads.daemon" : 19,
    "threads" : 22,
    "classes" : 5819,
    "classes.loaded" : 5819,
    "classes.unloaded" : 0,
    "gc.ps_scavenge.count" : 7,
    "gc.ps_scavenge.time" : 54,
    "gc.ps_marksweep.count" : 1,
    "gc.ps_marksweep.time" : 44,
    "httpsessions.max" : -1,
    "httpsessions.active" : 0,
    "counter.status.200.root" : 1,
    "gauge.response.root" : 37.0
}
```

Custom Endpoint
--------------------
First, we need to have the new endpoint implement the Endpoint<T> interface:


```java
@Component
public class CustomEndpoint implements Endpoint<List<String>> {
    
    @Override
    public String getId() {
        return "customEndpoint";
    }

    @Override
    public boolean isEnabled() {
        return true;
    }

    @Override
    public boolean isSensitive() {
        return true;
    }

    @Override
    public List<String> invoke() {
        // Custom logic to build the output
        List<String> messages = new ArrayList<String>();
        messages.add("This is message 1");
        messages.add("This is message 2");
        return messages;
    }
}
```
In order to access this new endpoint, its id is used to map it. In other words we could exercise it hitting /customEndpoint.

Output:
```log
[ "This is message 1", "This is message 2" ]
```

Building an Application with Spring Boot
---------------


Spring Boot does not generate code or make edits to your files. Instead, when you start your application, Spring Boot dynamically wires up beans and settings and applies them to your application context.

Starting with Spring Initializer
---------------
- Go to https://start.spring.io. This service pulls in all the dependencies you need for an application and does most of the setup for you.
- Choose either Gradle or Maven and the language you want to use. This guide assumes that you chose Java.
- Click Dependencies and select Spring Web.
- Click Generate.
- Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.

Create a Simple Web Application
---------------

Now you can create a web controller for a simple web application

```java
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
public class HelloController {
	@RequestMapping("/")
	public String index() {
		return "Greetings from Spring Boot!";
	}
}
```

The class is marked as a `@RestController`, meaning it is ready for use by Spring MVC to handle web requests. @RequestMapping maps `/` to the index() method. When invoked from a browser or by using curl on the command line, the method returns pure text. That is because @RestController combines @Controller and @ResponseBody, two annotations that results in web requests returning data rather than a view.

Create an Application class
---------------
The Spring Initializr creates a simple application class for you. However, in this case, it is too simple. You need to modify the application class to match the(from src/main/java/com/example/springboot/Application.java):

```java
package com.example.springboot;
import java.util.Arrays;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
@SpringBootApplication
public class Application {
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
	@Bean
	public CommandLineRunner commandLineRunner(ApplicationContext ctx) {
		return args -> {
			System.out.println("Let's inspect the beans provided by Spring Boot:");
			String[] beanNames = ctx.getBeanDefinitionNames();
			Arrays.sort(beanNames);
			for (String beanName : beanNames) {
				System.out.println(beanName);
			}
		};
	}
}
```
@SpringBootApplication  annotation that adds:

- `@Configuration`: Tags the class as a source of bean definitions for the application context.
- `@EnableAutoConfiguration`: Tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings. For example, if spring-webmvc is on the classpath, this annotation flags the application as a web application and activates key behaviors, such as setting up a DispatcherServlet.
- `@ComponentScan`: Tells Spring to look for other components, configurations, and services in the com/example package, letting it find the controllers.


The main() method uses Spring Boot’s `SpringApplication.run()` method to launch an application.There is no web.xml file. This web application is 100% pure Java and you did not have to deal with configuring any plumbing or infrastructure.

There is also a `CommandLineRunner` method marked as a `@Bean`, and this runs on start up. It retrieves all the beans that were created by your application or that were automatically added by Spring Boot. 

Run the Application
---------------

Add Unit Tests
---------------

Add Production-grade Services
---------------



For more information:

1. [Spring Boot Actuator](https://www.baeldung.com/spring-boot-actuators)
2. [Getting Started with Spring Boot](https://www.javaguides.net/2018/09/getting-started-with-spring-boot.html)
3. [Building an Application with Spring Boot](https://spring.io/guides/gs/spring-boot/)



