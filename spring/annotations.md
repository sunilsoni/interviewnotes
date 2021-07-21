Annotations
==========

@Autowired
----------

Since version 2.5, Spring provides the @Autowired annotation to discover the beans automatically and inject collaborating beans (other associated dependent beans) into our bean.

By declaring all the beans in Spring Configuration file, Spring container can autowire relationships between collaborating beans. 

After enabling annotation based injection, now we can use @Autowired annotation. @Autowired can be used on following injection points.

1. Constructors
2. Methods
3. Fields and
4. Parameters

and dependencies can be injected using by type OR by name OR by @Qualifier.


In spring there are two types of autowiring. Those are
- **Autowiring by type** : @Autowired by type uses the class type to autowire the spring boot bean class. The bean is autowired based on the type of the variable.
- **Autowiring by name** : For Autowiring by name, the name of the variable is used for the dependency injection. The name of the authoring variable should be the same as the name of the class or the bean name configured in the @Component annotation.

For example,

```java
public interface Shape {
	public void draw();
}

@Component
public class Rectangle implements Shape {
	@Override
	public void draw() {
		System.out.println(">>>>>>>>>>>>>INVOKING THE RECTANGLE INSTANCE<<<<<<<<<<<<<<<<");
	}
}

@Component
public class Circle implements Shape{
	@Override
	public void draw() {
		System.out.println(">>>>>>>>>>>>>INVOKING THE CIRCLE INSTANCE<<<<<<<<<<<<<<<<");
	}
}

```
the shape interface is implemented by two classes Circle and Rectangle. So we can say both are instances of Shape or both shape. It made Rectangle and Circle as spring beans using the annotation @Component. Now let's see how to autowire these beans in another class.

```java
@Component
public class ShapeService {
	@Autowired
	private Shape rectangle;//by name
	
	@Autowired
	private Rectangle myRectangle;//by type

}
```

Here in ShapeService class, it is autowring the shape Rectangle in two ways.
1. Here in the first @Autowiring, the variable rectangle is autowired based on the name of the variable. Here when the spring checks the type of the variable, he can see it is Shape. But there are two shape implementations are there Rectangle and Circle. So spring doesn't get a proper solution for what component need to autowire. Then the spring check the name of the variable(rectangle) and find out any Shape component with the same name is available. Yes…The Rectangle component is available. So the spring will inject the property with rectangle component.
2. In the second @Autowiring, the type of property is Rectangle. So the spring directly injects the Rectangle component to the property myRectangle.


@Inject vs @Autowired
---------------------

| Key       | @Inject                         |@Autowired                       |
|-----------------|-----------------------------------|-----------------|
|  Basic     | It is part of Java CDI(Contexts and Dependency Injection)   |  It is part of Spring framework  |
|  Required   |  It has no required attribute    |  It has required attribute   |
|  Default Scope   |    Default scope of the autowired beans is Singleton    | Default scope of the inject beans is prototype  |
|  Ambiguity  |  In case of ambiguity in beans for injection then @Named qualifier should be added in your code.  |   In case of ambiguity in beans for injection then @Qualifer  qualifier should be added in your code. |
|  Advantage   | It is a part of Java CDI so it is not dependent on any DI framework. It makes your system loosely coupled. | It makes your application tightly coupled with Spring framework. In the future , if you want to move to another DI framework then you need reconfigure your application.  |


Component Scanning
---------------------
To do dependency injection, Spring creates a so-called application context.

During startup, Spring instantiates objects and adds them to the application context. Objects in the application context are called “Spring beans” or “components”.

Spring resolves dependencies between Spring beans and injects Spring beans into other Spring beans’ fields or constructors.

The process of searching the classpath for classes that should contribute to the application context is called component scanning.

When developing Spring Boot applications, you need to tell the Spring Framework where to look for Spring components. Using component scan is one method of asking Spring to detect Spring managed components. Spring needs the information to locate and register all the Spring components with the application context when the application starts.

Spring can auto scan, detect, and instantiate components from pre-defined project packages. It can auto scan all classes annotated with the stereotype annotations @Component @Controller, @Service and @Repository


@ComponentScan
---------------
@ComponentScan tells Spring in which packages you have annotated classes which should be managed by Spring. So, for example, if you have a class annotated with @Controller which is in a package which is not scanned by Spring, you will not be able to use it as Spring controller.

Classes annotated with @Configuration is a new way of configuring Spring using annotations instead of XML files (it's called Java configuration). Spring needs to know which packages contain spring beans, otherwise you would have to register each bean individually. That's what @ComponentScan is used for.


@ComponentScan Without Arguments
---------------
we use the @ComponentScan annotation along with the @Configuration annotation to specify the packages that we want to be scanned. @ComponentScan without arguments tells Spring to scan the current package and all of its sub-packages.
```java
@Configuration
@ComponentScan
public class DemoAppConfig {
    //...
}
```

@ComponentScan With Arguments
---------------
```java
@Configuration
@ComponentScan(basePackages = {"basic.ioc.autowire", "basic.ioc.setter"})
public class AutowireBeanConfig {
    //other configs
}
```

@ComponentScan with Exclusions
---------------

Use a filter,with the pattern for the classes to exclude:

```java
    @Configuration
@ComponentScan(basePackages = "com.demo",
        includeFilters = @Filter(type = FilterType.REGEX, pattern = ".*Dao"),
        excludeFilters = @Filter(Repository.class))
public class AppConfig {
        ...
}
```

@ComponentScan in a Spring-Boot application
---------------
Spring-Boot application, we don’t need to specify the @Configuration annotation unless we want more control over the classpath scanning. This is because of the @SpringBootApplication , which is already a combination of below listed three annotations.

- @Configuration
- @EnableAutoConfiguration
- @ComponentScan



Difference between @Component, @Repository & @Service annotations?
---------------

From [Spring Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-stereotype-annotations):

Spring provides  stereotype annotations: @Component, @Service, and @Controller. @Component is a generic stereotype for any Spring-managed component. @Repository, @Service, and @Controller are specializations of @Component for more specific use cases (in the persistence, service, and presentation layers, respectively). Therefore, you can annotate your component classes with @Component, but, by annotating them with @Repository, @Service, or @Controller instead, your classes are more properly suited for processing by tools or associating with aspects.

@Repository
-----------
stereotype for persistence layer

@Repository’s job is to catch persistence-specific exceptions and re-throw them as one of Spring’s unified unchecked exceptions.

For this, Spring provides `PersistenceExceptionTranslationPostProcessor`, which we are required to add in our application context (already included if we're using Spring Boot):
```java
<bean class="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor"/>
```
This bean post processor adds an advisor to any bean that’s annotated with @Repository.

@Service
---------
stereotype for service layer

We mark beans with @Service to indicate that they're holding the business logic. Besides being used in the service layer, there isn't any other special use for this annotation.

@Controller
-----------
stereotype for presentation layer (spring-mvc)

Instead of using @Component on a controller class in Spring MVC, we use @Controller, which is more readable and appropriate.

By using that annotation we do two things, first, we declare that this class is a Spring bean and should be created and maintained by Spring ApplicationContext, but also we indicate that its a controller in MVC setup. This latter property is used by web-specific tools and functionalities.

For example, DispatcherServlet will look for @RequestMapping on classes that are annotated using @Controller but not with @Component.

This means @Component and @Controller are the same with respect to bean creation and dependency injection but later is a specialized form of former. Even if you replace @Controller annotation with @Compoenent, Spring can automatically detect and register the controller class but it may not work as you expect with respect to request mapping.



For more information:

1. [Spring – @Autowired](https://javabydeveloper.com/tutorial-on-spring-autowired/)
2. [Core Spring Framework Annotations](https://medium.com/javarevisited/core-spring-framework-annotations-300493ba85da)
3. [Spring Component Scanning](https://www.baeldung.com/spring-component-scanning)
4. [Classpath Scanning using @ComponentScan and Filters](https://jstobigdata.com/spring/classpath-scanning-using-componentscan-and-filters/)