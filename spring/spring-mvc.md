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









