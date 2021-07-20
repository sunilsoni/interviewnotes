Annotations
==========



@Inject vs @Autowired
---------------------

| Key       | @Inject                         |@Autowired                       |
|-----------------|-----------------------------------|-----------------|
|  Basic     | It is part of Java CDI(Contexts and Dependency Injection)   |  It is part of Spring framework  |
|  Required   |  It has no required attribute    |  It has required attribute   |
|  Default Scope   |    Default scope of the autowired beans is Singleton    | Default scope of the inject beans is prototype  |
|  Ambiguity  |  In case of ambiguity in beans for injection then @Named qualifier should be added in your code.  |   In case of ambiguity in beans for injection then @Qualifer  qualifier should be added in your code. |
|  Advantage   | It is a part of Java CDI so it is not dependent on any DI framework. It makes your system loosely coupled. | It makes your application tightly coupled with Spring framework. In the future , if you want to move to another DI framework then you need reconfigure your application.  |






