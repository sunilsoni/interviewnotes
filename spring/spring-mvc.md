Spring MVC
==========

Spring MVC flow
--------------
In Spring Web MVC, `DispatcherServlet` class works as the front controller. It is responsible to manage the flow of the spring mvc application.

The `@Controller` annotation is used to mark the class as the controller in Spring 3.

The `@RequestMapping` annotation is used to map the request url. It is applied on the method.

Spring MVC Execution Flow
--------------
- **Step 1:** First request will be received by DispatcherServlet.
- **Step 2:** DispatcherServlet will take the help of HandlerMapping and get to know the Controller class name associated with the given request.
- **Step 3:** So request transfer to the Controller, and then controller will process the request by executing appropriate methods and returns ModelAndView object (contains Model data and View name) back to the DispatcherServlet.
- **Step 4:** Now DispatcherServlet send the model object to the ViewResolver to get the actual view page.
- **Step 5:** Finally DispatcherServlet will pass the Model object to the View page to display the result.

 <img src="./images/spring-mvc-flow.png" width="500" border="2" />


Spring Web Annotations
--------------

@RequestMapping
--------------

it can be configured using:

- path, or its aliases, name, and value: which URL the method is mapped to
- method: compatible HTTP methods
- params: filters requests based on presence, absence, or value of HTTP parameters
- headers: filters requests based on presence, absence, or value of HTTP headers
- consumes: which media types the method can consume in the HTTP request body
- produces: which media types the method can produce in the HTTP response body

Example: 
```java
@Controller
class VehicleController {

    @RequestMapping(value = "/vehicles/home", method = RequestMethod.GET)
    String home() {
        return "home";
    }
}
```

this configuration has the same effect :

```java
@Controller
@RequestMapping(value = "/vehicles", method = RequestMethod.GET)
class VehicleController {

    @RequestMapping("/home")
    String home() {
        return "home";
    }
}

```

Moreover, @GetMapping, @PostMapping, @PutMapping, @DeleteMapping, and @PatchMapping are different variants of @RequestMapping with the HTTP method already set to GET, POST, PUT, DELETE, and PATCH respectively.

These are available since Spring 4.3 release.

@RequestBody
-----------
maps the body of the HTTP request to an object.The deserialization is automatic and depends on the content type of the request.
```java
@PostMapping("/save")
void saveVehicle(@RequestBody Vehicle vehicle) {
    // ...
}
```

@PathVariable
-----------
This annotation indicates that a method argument is bound to a URI template variable. We can specify the URI template with the @RequestMapping annotation and bind a method argument to one of the template parts with @PathVariable.

We can achieve this with the name or its alias, the value argument:
```java
@RequestMapping("/{id}")
Vehicle getVehicle(@PathVariable("id") long id) {
    // ...
}
```
If the name of the part in the template matches the name of the method argument, we don't have to specify it in the annotation:
```java
@RequestMapping("/{id}")
Vehicle getVehicle(@PathVariable long id) {
    // ...
}
```
Moreover, we can mark a path variable optional by setting the argument required to false:

```java
@RequestMapping("/{id}")
Vehicle getVehicle(@PathVariable(required = false) long id) {
    // ...
}

```

@RequestParam
-----------
We use @RequestParam for accessing HTTP request parameters:


```java
@RequestMapping
Vehicle getVehicleByParam(@RequestParam("id") long id) {
    // ...
}
```
It has the same configuration options as the @PathVariable annotation.

In addition to those settings, with @RequestParam we can specify an injected value when Spring finds no or empty value in the request. To achieve this, we have to set the defaultValue argument.

Providing a default value implicitly sets required to false:
```java
@RequestMapping("/buy")
Car buyCar(@RequestParam(defaultValue = "5") int seatCount) {
    // ...
}
```

Response Handling Annotations

@ResponseBody
-----------
If we mark a request handler method with @ResponseBody, Spring treats the result of the method as the response itself:
```java
@ResponseBody
@RequestMapping("/hello")
String hello() {
    return "Hello World!";
}
```

@ExceptionHandler
-----------
With this annotation, we can declare a custom error handler method. Spring calls this method when a request handler method throws any of the specified exceptions.

The caught exception can be passed to the method as an argument:
```java
@ExceptionHandler(IllegalArgumentException.class)
void onIllegalArgumentException(IllegalArgumentException exception) {
    // ...
}
```

@ResponseStatus
-----------
We can specify the desired HTTP status of the response if we annotate a request handler method with this annotation. We can declare the status code with the code argument, or its alias, the value argument.

Also, we can provide a reason using the reason argument.

We also can use it along with @ExceptionHandler:

```java
@ExceptionHandler(IllegalArgumentException.class)
@ResponseStatus(HttpStatus.BAD_REQUEST)
void onIllegalArgumentException(IllegalArgumentException exception) {
    // ...
}
```

Other Web Annotations

@Controller
-----------
We can define a Spring MVC controller with @Controller.@Controller is a class level annotation which tells the Spring Framework that this class serves as a controller in Spring MVC:
```java
@Controller
public class VehicleController {
    // ...
}
```

@RestController
-----------
The @RestController combines @Controller and @ResponseBody.

```java
@Controller
@ResponseBody
class VehicleRestController {
    // ...
}
```

is same as :
```java
@RestController
class VehicleRestController {
    // ...
}
```

@ModelAttribute
-----------
With this annotation we can access elements that are already in the model of an MVC @Controller, by providing the model key:
```java
@PostMapping("/assemble")
void assembleVehicle(@ModelAttribute("vehicle") Vehicle vehicleInModel) {
    // ...
}
```

Like with @PathVariable and @RequestParam, we don't have to specify the model key if the argument has the same name:
```java
@PostMapping("/assemble")
void assembleVehicle(@ModelAttribute Vehicle vehicle) {
    // ...
}
```
Besides, @ModelAttribute has another use: if we annotate a method with it, Spring will automatically add the method's return value to the model:
```java
@ModelAttribute("vehicle")
Vehicle getVehicle() {
    // ...
}
```
Like before, we don't have to specify the model key, Spring uses the method's name by default:
```java
@ModelAttribute
Vehicle vehicle() {
    // ...
}

```
Before Spring calls a request handler method, it invokes all @ModelAttribute annotated methods in the class.



@CrossOrigin
-----------
@CrossOrigin enables cross-domain communication for the annotated request handler methods:
If we mark a class with it, it applies to all request handler methods in it.

```java
@CrossOrigin
@RequestMapping("/hello")
String hello() {
    return "Hello World!";
}
```


For more information:

1. [Spring MVC flow with Example](https://codenuclear.com/spring-mvc-flow-with-example/)
2. [Spring Web Annotations](https://www.baeldung.com/spring-mvc-annotations)


