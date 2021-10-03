API Gateway
===========

API Gateway is a special class of microservices that meets the need of a single client application (such as android app, web app, angular JS app, iPhone app, etc) and provide it with single entry point to the backend resources (microservices), providing cross cutting concerns to them such as security, monitoring/metrics & resiliency

 <img src="./images-ms/API-Gateway.png" width="800" border="2" />

Client Application can access tens or hundreds of microservices concurrently with each request , aggregating the response and transforming them to meet the client application’s needs. Api Gateway can use a client side load balancer library (Ribbon) to distribute load across instances based on round-robin fashion. It can also do protocol translation i.e. HTTP to AMQP if necessary. It can handle security for the protected resources as well.

1. Spring Cloud DiscoveryClient integration
2. Declare intelligent routing for services, like:

```yaml
info.component: API Gateway
zuul.routes:
  customer-service:
    path: /customer/**
    serviceId: customer-service
  product-service:
    path: /product/**
    serviceId: product-service
```
customer-service is the application name of customer microservice, and fetched from eureka service registry using DiscoveryClient.

3. Request Rate Limiting (available in Spring Boot 2.x)
4. Path Rewriting
5. Hystrix Circuit Breaker integration for resiliency

















