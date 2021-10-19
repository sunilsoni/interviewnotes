Spring Boot
===========

Spring Boot is an opinionated addition to the Spring platform, focused on convention over configuration — highly useful for getting started with minimum effort and creating standalone, production-grade applications.

Spring Boot is basically an extension of the Spring framework which eliminated the boilerplate configurations required for setting up a Spring application.

Spring Boot is an opinionated framework that helps developers build Spring-based applications quickly and easily. The main goal of Spring Boot is to quickly create Spring-based applications without requiring developers to write the same boilerplate configuration again and again.

Spring Boot Primary Goals
-------------------------

- Provide a radically faster and widely accessible getting-started experience for all Spring development.
- Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
- Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
- Absolutely no code generation and no requirement for XML configuration.

Key Spring Boot features
------------------------

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

Spring Boot comes with over 40 different starter modules, which provide ready-to-use integration libraries for many different frameworks, such as database connections that are both relational and NoSQL, web services, social network integration, monitoring libraries, logging, template rendering, and so on.


| Starter                      | Description                                                                                                                                                                                                                                                                                                                               |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| spring-boot-starter          | This is the core Spring Boot starter that provides you with all the foundational functionalities. It is depended upon by all other starters, so there is no need to declare it explicitly.                                                                                                                                                |
| spring-boot-starter-actuator | This starter provides you with a functionality to monitor, manage an application, and audit it.                                                                                                                                                                                                                                           |
| spring-boot-starter-jdbc     | This starter provides you with a support to connect and use JDBC databases, connection pools, and so on.                                                                                                                                                                                                                                  |
| spring-boot-starter-data-jpa | The JPA starter provides you with needed libraries in order to use Java Persistence API such as Hibernate, and others.                                                                                                                                                                                                                    |
| spring-boot-starter-data-*   | Collection of data-* family starter components providing support for a number of data stores such as MongoDB, Data-Rest, or Solr.                                                                                                                                                                                                         |
| spring-boot-starter-security | This brings in all the needed dependencies for spring-security.                                                                                                                                                                                                                                                                           |
| spring-boot-starter-social-* | This provides you with integration with Facebook, Twitter, and LinkedIn.                                                                                                                                                                                                                                                                  |
| spring-boot-starter-test     | This is a starter that contains the dependencies for spring-test and assorted testing frameworks such as JUnit and Mockito among others.                                                                                                                                                                                                  |
| spring-boot-starter-web      | This gives you all the needed dependencies for web application development. It can be complimented with spring-boot-starter-hateoas, spring-boot-starter-websocket, spring-boot-starter-mobile, or spring-boot-starter-ws, and assorted template rendering starters such as sping-boot-starter-thymeleaf or spring-boot-starter-mustache. |

Spring Boot Autoconfiguration
-----------------------------

Spring Boot addresses the problem that Spring applications need complex configuration by eliminating the need to manually set up the boilerplate configuration.
Spring Boot takes an opinionated view of the application and configures various components automatically, by registering beans based on various criteria. The criteria can be:

- Availability of a particular class in a classpath
- Presence or absence of a Spring bean
- Presence of a system property
- An absence of a configuration file

`For example,` if you have the spring-webmvc dependency in your classpath, Spring Boot assumes you are trying to build a SpringMVC-based web application and automatically tries to register DispatcherServlet if it is not already registered. If you have any embedded database drivers in the classpath, such as H2 or HSQL, and if you haven’t configured a DataSource bean explicitly, then Spring Boot will automatically register a DataSource bean using in-memory database settings.

Easy-to-Use Embedded Servlet Container Support
----------------------------------------------

Traditionally, while building web applications, you need to create WAR type modules and then deploy them on external servers like Tomcat, WildFly, etc. But by using Spring Boot, you can create a JAR type module and embed the servlet container in the application very easily so that the application will be a self-contained deployment unit.

Also, during development, you can easily run the Spring Boot JAR type module as a Java application from the IDE or from the command-line using a build tool like Maven or Gradle.

Spring Boot Annotations
-----------------------

@SpringBootApplication
----------------------

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
------------------------

@EnableAutoConfiguration, as its name says, enables auto-configuration. It means that Spring Boot looks for auto-configuration beans on its classpath and automatically applies them.

Note, that we have to use this annotation with @Configuration:

```java
@Configuration
@EnableAutoConfiguration
class MyConfig {
  
}
```

@ConditionalOnClass and @ConditionalOnMissingClass
--------------------------------------------------

Using these conditions, Spring will only use the marked auto-configuration bean if the class in the annotation's argument is present/absent:

```java
@Configuration
@ConditionalOnClass(DataSource.class)
class MySQLAutoconfiguration {
    //...
}
```

@ConditionalOnBean and @ConditionalOnMissingBean
------------------------------------------------

We can use these annotations when we want to define conditions based on the presence or absence of a specific bean:

```java
@Bean
@ConditionalOnBean(name = "dataSource")
LocalContainerEntityManagerFactoryBean entityManagerFactory() {
        // ...
}
```

@ConditionalOnProperty
----------------------

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
----------------------

We can make Spring to use a definition only when a specific resource is present:

```java
@ConditionalOnResource(resources = "classpath:mysql.properties")
Properties additionalProperties() {
        // ...
}
```

@ConditionalOnWebApplication and @ConditionalOnNotWebApplication
----------------------------------------------------------------

With these annotations, we can create conditions based on if the current application is or isn't a web application:

```java
@ConditionalOnWebApplication
HealthCheckController healthCheckController() {
        // ...
}
```

@ConditionalExpression
----------------------

We can use this annotation in more complex situations. Spring will use the marked definition when the SpEL expression is evaluated to true:

```java
@Bean
@ConditionalOnExpression("${usemysql} && ${mysqlserver == 'local'}")
DataSource dataSource() {
        // ...
}
```

@Conditional
------------

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
-------------------------------------

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
--------------

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
-----------------

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
---------------

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
----------------------------------------

Spring Boot does not generate code or make edits to your files. Instead, when you start your application, Spring Boot dynamically wires up beans and settings and applies them to your application context.

Starting with Spring Initializer
--------------------------------

- Go to https://start.spring.io. This service pulls in all the dependencies you need for an application and does most of the setup for you.
- Choose either Gradle or Maven and the language you want to use. This guide assumes that you chose Java.
- Click Dependencies and select Spring Web.
- Click Generate.
- Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.

Create a Simple Web Application
-------------------------------

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
---------------------------

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
-------------------

To run the application use `mvnw spring-boot:run` command or for gradle `./gradlew bootRun`

You should see output similar to the following:

```log
Let's inspect the beans provided by Spring Boot:
application
beanNameHandlerMapping
defaultServletHandlerMapping
dispatcherServlet
embeddedServletContainerCustomizerBeanPostProcessor
handlerExceptionResolver
helloController
httpRequestHandlerAdapter
messageSource
mvcContentNegotiationManager
mvcConversionService
mvcValidator
org.springframework.boot.autoconfigure.MessageSourceAutoConfiguration
org.springframework.boot.autoconfigure.PropertyPlaceholderAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$DispatcherServletConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$EmbeddedTomcat
org.springframework.boot.autoconfigure.web.ServerPropertiesAutoConfiguration
org.springframework.boot.context.embedded.properties.ServerProperties
org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor
org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor
org.springframework.context.annotation.internalAutowiredAnnotationProcessor
org.springframework.context.annotation.internalCommonAnnotationProcessor
org.springframework.context.annotation.internalConfigurationAnnotationProcessor
org.springframework.context.annotation.internalRequiredAnnotationProcessor
org.springframework.web.servlet.config.annotation.DelegatingWebMvcConfiguration
propertySourcesBinder
propertySourcesPlaceholderConfigurer
requestMappingHandlerAdapter
requestMappingHandlerMapping
resourceHandlerMapping
simpleControllerHandlerAdapter
tomcatEmbeddedServletContainerFactory
viewControllerHandlerMapping
```

You can clearly see `org.springframework.boot.autoconfigure` beans. There is also a tomcatEmbeddedServletContainerFactory.

Now run the service with curl (in a separate terminal window), by running the  command:

```log
$ curl localhost:8080
Greetings from Spring Boot!
```

Add Unit Tests
--------------

add the  dependency to your `pom.xml` file:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-test</artifactId>
	<scope>test</scope>
</dependency>
```

Now write a simple unit test that mocks the servlet request and response through your endpoint:

```java
package com.example.springboot;

import static org.hamcrest.Matchers.equalTo;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

@SpringBootTest
@AutoConfigureMockMvc
public class HelloControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void getHello() throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("Greetings from Spring Boot!")));
    }
}
```

`MockMvc` comes from Spring Test and you can send HTTP requests into the `DispatcherServlet` and make assertions about the result. Having used `@SpringBootTest`, we are asking for the whole application context to be created. An alternative would be to ask Spring Boot to create only the web layers of the context by using `@WebMvcTest`. In either case, Spring Boot automatically tries to locate the main application class of your application, but you can override it or narrow it down if you want to build something different.

We can also use Spring Boot to write a simple full-stack integration test. For example,

```java
package com.example.springboot;

import static org.assertj.core.api.Assertions.*;

import java.net.URL;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.boot.web.server.LocalServerPort;
import org.springframework.http.ResponseEntity;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class HelloControllerIT {

	@LocalServerPort
	private int port;

	private URL base;

	@Autowired
	private TestRestTemplate template;

    @BeforeEach
    public void setUp() throws Exception {
        this.base = new URL("http://localhost:" + port + "/");
    }

    @Test
    public void getHello() throws Exception {
        ResponseEntity<String> response = template.getForEntity(base.toString(),
                String.class);
        assertThat(response.getBody()).isEqualTo("Greetings from Spring Boot!");
    }
}
```

The embedded server starts on a random port because of webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT, and the actual port is discovered at runtime with @LocalServerPort.

Add Production-grade Services
-----------------------------

Spring Boot provides several such services (such as health, audits, beans, and more) with its actuator module.
add the  dependency to your pom.xml file:

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

We should see that a new set of RESTful end points have been added to the application. These are management services provided by Spring Boot.

The actuator exposes the endpoints like:

- actuator/health
- actuator/info
- actuator

Running Spring boot app at different port on server startup
-----------------------------------------------------------

**Why do we need that?**
If we want to run multiple instances of single app on same server, then we need to assign a different port at runtime. To solve this problem we need to choose random available port at app startup. Since the app will register itself with eureka service registry, other apps can still discover this service through service registry.

Spring boot provides a convenient class to determine if a port is available or not.

**Assigning a random port in custom port range**

Utility class that search available port in custom range.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.util.SocketUtils;
import org.springframework.util.StringUtils;
public class SpringBootUtil {
    final static Logger log = LoggerFactory.getLogger(SpringBootUtil.class);
    public static void setRandomPort(int minPort, int maxPort) {
    try {
        String userDefinedPort = System.getProperty("server.port", System.getenv("SERVER_PORT
        if(StringUtils.isEmpty(userDefinedPort)) {
            int port = SocketUtils.findAvailableTcpPort(minPort, maxPort);
            System.setProperty("server.port", String.valueOf(port));
            log.info("Random Server Port is set to {}.", port);
        }
    } catch( IllegalStateException e) {
        log.warn("No port available in range 5000-5100. Default embedded server configuration
    }
    }
}

```

**Spring Boot Main Application.**

```java
public class Application {
    private static final Logger logger = LoggerFactory.getLogger(Application.class);
    public static void main(String[] args) {
        SpringBootUtil.setRandomPort(5000, 5500);
        ApplicationContext ctx = SpringApplication.run(Application.class, args);
        logger.info("Application " + ctx.getApplicationName() + " started");
    }
...
}

```

Calling the custom method to set the random available port within range [5000-5500]  and update the server.port property as well.

**Tip**
Always use Eureka Registry to fetch the service details e.g. host, port and protocol. Never use hardcoded host, port while communicating with one microservice from another. So you never need to know in advance what port and host a particular service has been deployed.

# Spring Boot CRUD Web Application with Thymeleaf, Spring MVC, Spring Data JPA, Hibernate, MySQL

##  Create Spring Boot Project


Step 1: Open Spring Initializr http://start.spring.io.

Step 2: Select the Spring Boot version 2.4.0.

Step 2: Provide the Group name.

Step 3: Provide the Artifact Id. 

Step 5: Add the dependencies Spring Web, Spring Data JPA, and H2/MySQL Database.

Step 6: Click on the Generate button. When we click on the Generate button, it wraps the specifications in a Jar file and downloads it to the local system.

##  Maven Dependencies

pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.7.RELEASE</version>
        <relativePath/>
        <!-- lookup parent from repository -->
    </parent>
    <groupId>net.javaguides</groupId>
    <artifactId>springboot-thymeleaf-crud-web-app</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot-thymeleaf-crud-web-app</name>
    <description>Demo project for Spring Boot and thymeleaf</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```
##  Configure and Setup MySQL Database

application.properties

```properties
server.port=8888

spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/users_database?useSSL=false
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=update
```

##  Model Layer - Create JPA Entity - 

  Employee.java  Let's create User model or domain class with following fields:

   **id** - primary key

   **firstName** - user first name

   **lastName** - user last name

   **emailId** - user email ID

   **createdAt** - user object created date

   **createdBy** - use object created by

   **updatedAt** - user object updated by

   **updatedby** - user object updated by


```java
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "employees")
@Setter
@Getter
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

```


##  Repository Layer - EmployeeRepository.java

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import net.javaguides.springboot.model.Employee;

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long>{

}

```

##  Service Layer

```java
import java.util.List;

import net.javaguides.springboot.model.Employee;

public interface EmployeeService {
    List < Employee > getAllEmployees();
    void saveEmployee(Employee employee);
    Employee getEmployeeById(long id);
    void deleteEmployeeById(long id);
}

```


```java

import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import net.javaguides.springboot.model.Employee;
import net.javaguides.springboot.repository.EmployeeRepository;

@Service
public class EmployeeServiceImpl implements EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    @Override
    public List < Employee > getAllEmployees() {
        return employeeRepository.findAll();
    }

    @Override
    public void saveEmployee(Employee employee) {
        this.employeeRepository.save(employee);
    }

    @Override
    public Employee getEmployeeById(long id) {
        Optional < Employee > optional = employeeRepository.findById(id);
        Employee employee = null;
        if (optional.isPresent()) {
            employee = optional.get();
        } else {
            throw new RuntimeException(" Employee not found for id :: " + id);
        }
        return employee;
    }

    @Override
    public void deleteEmployeeById(long id) {
        this.employeeRepository.deleteById(id);
    }
}

```
##  Controller Layer - EmployeeController.java


```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;

import net.javaguides.springboot.model.Employee;
import net.javaguides.springboot.service.EmployeeService;

@Controller
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    // display list of employees
    @GetMapping("/")
    public String viewHomePage(Model model) {
        model.addAttribute("listEmployees", employeeService.getAllEmployees());
        return "index";
    }

    @GetMapping("/showNewEmployeeForm")
    public String showNewEmployeeForm(Model model) {
        // create model attribute to bind form data
        Employee employee = new Employee();
        model.addAttribute("employee", employee);
        return "new_employee";
    }

    @PostMapping("/saveEmployee")
    public String saveEmployee(@ModelAttribute("employee") Employee employee) {
        // save employee to database
        employeeService.saveEmployee(employee);
        return "redirect:/";
    }

    @GetMapping("/showFormForUpdate/{id}")
    public String showFormForUpdate(@PathVariable(value = "id") long id, Model model) {

        // get employee from the service
        Employee employee = employeeService.getEmployeeById(id);

        // set employee as a model attribute to pre-populate the form
        model.addAttribute("employee", employee);
        return "update_employee";
    }

    @GetMapping("/deleteEmployee/{id}")
    public String deleteEmployee(@PathVariable(value = "id") long id) {

        // call delete employee method 
        this.employeeService.deleteEmployeeById(id);
        return "redirect:/";
    }
}

```



##  View Layer: Thymeleaf
   
Create new `index.html` file under "resources/templates" folder and add the following content to it:


```haml
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">

<head>
    <meta charset="ISO-8859-1">
    <title>Employee Management System</title>

    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

</head>

<body>

    <div class="container my-2">
        <h1>Employees List</h1>

        <a th:href="@{/showNewEmployeeForm}" class="btn btn-primary btn-sm mb-3"> Add Employee </a>

        <table border="1" class="table table-striped table-responsive-md">
            <thead>
                <tr>
                    <th>Employee First Name</th>
                    <th>Employee Last Name</th>
                    <th>Employee Email</th>
                    <th> Actions </th>
                </tr>
            </thead>
            <tbody>
                <tr th:each="employee : ${listEmployees}">
                    <td th:text="${employee.firstName}"></td>
                    <td th:text="${employee.lastName}"></td>
                    <td th:text="${employee.email}"></td>
                    <td> <a th:href="@{/showFormForUpdate/{id}(id=${employee.id})}" class="btn btn-primary">Update</a>
                        <a th:href="@{/deleteEmployee/{id}(id=${employee.id})}" class="btn btn-danger">Delete</a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</body>

</html>

```


##  Run Spring application and demo

```bash
$ mvn spring-boot:run
```
SpringApplication is a static class that has a static method run, which takes two arguments our main class and the command-line argument for the main method.

What `@SpringBootApplication` annotation does ?

1). Set up the default configuration

2). Starts Spring Application Context

3). Performs a class-path scan

4). Starts Tomcat server

- Firstly, the application starts with a simple Java public static main method.
- Next, Spring starts your Spring context by looking up the auto-config initializers, configurations, and annotations that direct how to initialize and start up the Spring context.
- Lastly, it starts and auto-configures an embedded web server. The default application server is Tomcat for Spring Boot.


## Unit Testing REST APIs


```java
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertNotNull;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.boot.web.server.LocalServerPort;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.web.client.HttpClientErrorException;

import com.companyname.springbootcrudrest.SpringBootCrudRestApplication;
import com.companyname.springbootcrudrest.model.User;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = SpringBootCrudRestApplication.class, webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class SpringBootCrudRestApplicationTests {

    @Autowired
    private TestRestTemplate restTemplate;

    @LocalServerPort
    private int port;

    private String getRootUrl() {
        return "http://localhost:" + port;
    }

    @Test
    public void contextLoads() {

    }

    @Test
    public void testGetAllUsers() {
         HttpHeaders headers = new HttpHeaders();
         HttpEntity<String> entity = new HttpEntity<String>(null, headers);

         ResponseEntity<String> response = restTemplate.exchange(getRootUrl() + "/users",
         HttpMethod.GET, entity, String.class);
  
         assertNotNull(response.getBody());
    }

    @Test
    public void testGetUserById() {
        User user = restTemplate.getForObject(getRootUrl() + "/users/1", User.class);
        System.out.println(user.getFirstName());
        assertNotNull(user);
    }

    @Test
    public void testCreateUser() {
        User user = new User();
        user.setEmailId("admin@gmail.com");
        user.setFirstName("admin");
        user.setLastName("admin");
        user.setCreatedBy("admin");
        user.setUpdatedby("admin");

        ResponseEntity<User> postResponse = restTemplate.postForEntity(getRootUrl() + "/users", user, User.class);
        assertNotNull(postResponse);
        assertNotNull(postResponse.getBody());
    }

    @Test
    public void testUpdatePost() {
         int id = 1;
         User user = restTemplate.getForObject(getRootUrl() + "/users/" + id, User.class);
         user.setFirstName("admin1");
         user.setLastName("admin2");

         restTemplate.put(getRootUrl() + "/users/" + id, user);

         User updatedUser = restTemplate.getForObject(getRootUrl() + "/users/" + id, User.class);
         assertNotNull(updatedUser);
    }

    @Test
    public void testDeletePost() {
         int id = 2;
         User user = restTemplate.getForObject(getRootUrl() + "/users/" + id, User.class);
         assertNotNull(user);

         restTemplate.delete(getRootUrl() + "/users/" + id);
    
         try {
              user = restTemplate.getForObject(getRootUrl() + "/users/" + id, User.class);
         } catch (final HttpClientErrorException e) {
         assertEquals(e.getStatusCode(), HttpStatus.NOT_FOUND);
     }
  }

}



```
11. Extra or Additional features

 - How to enable JPA Auditing
 - Exception(Error) Handling for RESTful Services
 - Customizing Error Response Structure

Ref: 
https://github.com/RameshMF/springboot-thymeleaf-crud-pagination-sorting-webapp
https://www.javaguides.net/2018/09/spring-boot-2-hibernate-5-mysql-crud-rest-api-tutorial.html

## CrudRepository vs. JpaRepository





For more information:

1. [Spring Boot Actuator](https://www.baeldung.com/spring-boot-actuators)
2. [Getting Started with Spring Boot](https://www.javaguides.net/2018/09/getting-started-with-spring-boot.html)
3. [Building an Application with Spring Boot](https://spring.io/guides/gs/spring-boot/)
