Microservices
=================

Microservices - also known as the microservice architecture - is an architectural style that structures an application as a collection of services that are

- Highly maintainable and testable
- Loosely coupled
- Independently deployable
- Organized around business capabilities
- Owned by a small team

The microservice architecture enables the rapid, frequent and reliable delivery of large, complex applications. It also enables an organization to evolve its technology stack.

What is Micro Service?
> Micro Service is an architecture that allows the developers to develop and deploy services independently. Each service running has its own process and this achieves the lightweight model to support business applications.

 <img src="./images-ms/Beehive-Representation-Microservices.png" width="400" border="2" />


Advantages of Microservices Architecture
-----------------
|  Advantage       |  Description  |
| ----------- | ----------- |
| Independent Development |   All microservices can be easily developed based on their individual functionality |
| Independent Deployment |  Based on their services, they can be individually deployed in any application |
| Fault Isolation	 |   Even if one service of the application does not work, the system still continues to function |
| Mixed Technology Stack	 |  Different languages and technologies can be used to build different services of the same application |
| Granular Scaling	 |  Individual components can scale as per need, there is no need to scale all components together |

*  Microservices are self-contained, independent deployment module.
*  The cost of scaling is comparatively less than the monolithic architecture.
*  Microservices are independently manageable services. It can enable more and more services as the need arises. It minimizes the impact on existing service.
* It is possible to change or upgrade each service individually rather than upgrading in the entire application.
* Microservices allows us to develop an application which is organic (an application which latterly upgrades by adding more functions or modules) in nature.
* It enables event streaming technology to enable easy integration in comparison to heavyweight interposes communication.
* Microservices follows the single responsibility principle.
* The demanding service can be deployed on multiple servers to enhance performance.
* Less dependency and easy to test.
* Dynamic scaling.
* Faster release cycle.


Disadvantages of Microservices
-----------------
* Microservices has all the associated complexities of the distributed system.
* There is a higher chance of failure during communication between different services.
* Difficult to manage a large number of services.
* The developer needs to solve the problem, such as network latency and load balancing.
* Complex testing over a distributed environment.


Challenges of Microservices Architecture
-----------------
- **Bounded context**: The bounded context concept originated in Domain-Driven Design (DDD) circles. It promotes the Object model first approach to service, defining a data model that service is responsible for and is bound to. A bounded context clarifies, encapsulates, and defines the specific responsibility to the model. It ensures that the domain will not be distracted from the outside. Each model must have a context implicitly defined within a sub-domain, and every context defines boundaries. In other words, the service owns its data and is responsible for its integrity and mutability. It supports the most important feature of microservices, which is independence and decoupling.

- **Dynamic scale up and scale down**: The loads on the different microservices may be at a different instance of the type. As well as auto-scaling up your microservice should auto-scale down. It reduces the cost of the microservices. We can distribute the load dynamically.

- **Monitoring**: The traditional way of monitoring will not align well with microservices because we have multiple services making up the same functionality previously supported by a single application. When an error arises in the application, finding the root cause can be challenging.

- **Fault Tolerance**: Fault tolerance is the individual service that does not bring down the overall system. The application can operate at a certain degree of satisfaction when the failure occurs. Without fault tolerance, a single failure in the system may cause a total breakdown. The circuit breaker can achieve fault tolerance. The circuit breaker is a pattern that wraps the request to external service and detects when they are faulty. Microservices need to tolerate both internal and external failure.

- **Cyclic Dependency**: Dependency management across different services, and its functionality is very important. The cyclic dependency can create a problem, if not identified and resolved promptly.

- **DevOps Culture**: Microservices fits perfectly into the DevOps. It provides faster delivery service, visibility across data, and cost-effective data. It can extend their use of containerization switch from Service-Oriented-Architecture (SOA) to Microservice Architecture (MSA).

- The traditional logging is ineffective because microservices are stateless, distributed, and independent. The logging must be able to correlate events across several platforms.

- When more services interact with each other, the possibility of failure also increases.

Gateway
-----------------
>  Clients will not directly invoke microservices, they will go through the Gateway. The Gateway in turn can call the microservices and will return the response to the client.
   The Gateway can decouple the microservices from the clients. It will provide functions such as authentication, logging, load balancing etc.


Microservices Monitor
-----------------
> Spring Boot actuator will be a good tool monitor metrics, counters for individual microservices. But if we have multiple microservices, it is difficult to monitor each individually. We will use open source tools such as Prometheous, Kibana or Graphana for this . Prometheous is a pull based monitoring tool and it will contain metrics at provided intervals, displays them and will also trigger alerts. Kibana or Grafana are dashboard tools which are used for visualizing and monitor the data. When there will be large number of microservices with dependencies, we will use AppDynamics, Dynatrace, and New Relic that will draw dependencies among microservices.

Microservices vs Monolithic Architecture
-----------------

- **Microservices**
    - Service Startup is fast
    - Microservices are loosely coupled architecture.
    - Changes done in a single data model does not affect other Microservices.
    - Microservices focuses on products, not projects

- **Monolithic Architecture**
    - Service startup takes time
    - Monolithic architecture is mostly tightly coupled.
    - Any changes in the data model affect the entire database
    - Monolithic put emphasize over the whole project



How does Microservice Architecture work?
-----------------
A microservice architecture has the following components:

- **Clients** – Different users from various devices send requests.
- **Identity Providers** – Authenticates user or clients identities and issues security tokens.
- **API Gateway** – Handles client requests.
- **Static Content** – Houses all the content of the system.
- **Management** –  Balances services on nodes and identifies failures.
- **Service Discovery** – A guide to find the route of communication between microservices.
- **Content Delivery Networks** – Distributed network of proxy servers and their data centers.
- **Remote Service** – Enables the remote access information that resides on a network of IT devices.


<img src="./images-ms/microservice-architecture.png" width="500" border="2" />


Communicating Between Microservices
-----------------

There are two types of inter-service communication in Microservices:

 1. Synchronous communication : one service will communicate with another service through the rest endpoint using HTTP or https protocol. In this approach, calling service will wait until the caller service responds.
 2. Asynchronous communication : one service will communicate with another service through the asynchronous messaging. The calling service will not wait to respond by the caller service. First, it will return a response to the user, then the remaining services will process the request. Asynchronous communication in Microservices will be achieved through the messaging brokers like Apache Kafka, Apache ActiveMQ, etc.









For more information:
1. [Top 50 Microservices Interview Questions You Must Prepare In 2020](https://www.edureka.co/blog/interview-questions/microservices-interview-questions/)
2. [Top 25 Microservices Interview Questions and Answers](https://www.guru99.com/microservices-interview-questions.html)
3. [Microservices Tutorial](https://www.javatpoint.com/microservices)
4. [Microservices Inter-Service Communication](https://www.dineshonjava.com/microservices-inter-service-communication/)

