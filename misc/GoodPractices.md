Good Practices
=============


Good Practices for REST API Design
-----------------------------------

A REST API is an application programming interface that conforms to specific architectural constraints, like stateless
communication and cacheable data. It is not a protocol or standard. While REST APIs can be accessed through a number of
communication protocols, most commonly, they are called over HTTPS,


Accept and respond with JSON
----------------------------
REST APIs should accept JSON for request payload and also send responses to JSON. JSON is the standard for transferring
data. Almost every networked technology can use it

To make sure that when our REST API app responds with JSON that clients interpret it as such, we should
set `Content-Type` in the response header to `application/json`

Use nouns instead of verbs in endpoint paths
-----------------------------------
We shouldn’t use verbs in our endpoint paths. Instead, we should use the nouns which represent the entity that the
endpoint that we’re retrieving or manipulating as the pathname.

we should create routes like

- GET /articles/ for getting news articles. Likewise,
- POST /articles/ is for adding a new article ,
- PUT /articles/:id is for updating the article with the given id.
- DELETE /articles/:id is for deleting an existing article with the given ID.

Nesting resources for hierarchical objects
-----------------------------------
When designing endpoints, it makes sense to group those that contain associated information. That is, if one object can
contain another object, you should design the endpoint to reflect that.

For example, if we want an endpoint to get the comments for a news article, we should append the /comments path to the
end of the /articles path.


Handle errors gracefully and return standard error codes
-----------------------------------
we should handle errors gracefully and return HTTP response codes that indicate what kind of error occurred. This gives
maintainers of the API enough information to understand the problem that’s occurred. We don’t want errors to bring down
our system, so we can leave them unhandled, which means that the API consumer has to handle them.

Common error HTTP status codes include:

- **400 Bad Request** – This means that client-side input fails validation.
- **401 Unauthorized** – This means the user isn’t not authorized to access a resource. It usually returns when the user
  isn’t authenticated.
- **403 Forbidden** – This means the user is authenticated, but it’s not allowed to access a resource.
- **404 Not Found** – This indicates that a resource is not found.
- **500 Internal server error** – This is a generic server error. It probably shouldn’t be thrown explicitly.
- **502 Bad Gateway** – This indicates an invalid response from an upstream server.
- **503 Service Unavailable** – This indicates that something unexpected happened on server side (It can be anything
  like server overload, some parts of the system failed, etc.).

We should be throwing errors that correspond to the problem that our app has encountered. For example, if we want to
reject the data from the request payload, then we should return a 400 response


Allow filtering, sorting, and pagination
-----------------------------------
The databases behind a REST API can get very large. Sometimes, there’s so much data that it shouldn’t be returned all at
once because it’s way too slow or will bring down our systems. Therefore, we need ways to filter items.

We also need ways to paginate data so that we only return a few results at a time. We don’t want to tie up resources for
too long by trying to get all the requested data at once.

Filtering and pagination both increase performance by reducing the usage of server resources. As more data accumulates
in the database, the more important these features become.


Maintain Good Security Practices
-----------------------------------

Most communication between client and server should be private since we often send and receive private information.
Therefore, using SSL/TLS for security is a must.

People shouldn’t be able to access more information that they requested. For example, a normal user shouldn’t be able to
access information of another user. They also shouldn’t be able to access data of admins.

If we choose to group users into a few roles, then the roles should have the permissions that cover all they need and no
more.

Cache data to improve performance
-----------------------------------
We can add caching to return data from the local memory cache instead of querying the database to get the data every
time we want to retrieve some data that users request. The good thing about caching is that users can get data faster.
However, the data that users get may be outdated. This may also lead to issues when debugging in production environments
when something goes wrong as we keep seeing old data.

There are many kinds of caching solutions like Redis, in-memory caching,etc. We can change the way data is cached as our
needs change.

Versioning our APIs
--------------------

We should have different versions of API if we’re making any changes to them that may break clients. The versioning can
be done according to semantic version (for example, 2.0.6 to indicate major version 2 and the sixth patch) like most
apps do nowadays.

Versioning is usually done with /v1/, /v2/, etc. added at the start of the API path.


Java code review checklist
-------------------------

Code Quality
-------------------------

- Basic Checks (before)
    - The code compiles
    - Old unit tests pass
- The code was tested
    - The code was developer-tested
    - The new code must be covered by unit tests
    - Any refactoring must be covered by unit tests
    - At least 80% coverage for the code changes
- Clean Code
    - Naming Conventions (classes, constants, variables, methods (void vs return), etc)
    - No hard-coded variables
    - Indentation
    - No spelling mistakes
    - The code does what it says it does
    - The code is easy to read (**Readability**)
    - Avoid duplicate code
    - Check if the code could be replaced by calling functions in other libraries/components
- Best Practices
    - OOP Principles are correctly used
    - The code follows the SOLID PRINCIPLES
    - Design Patterns
        - Recommend a design pattern when you fill that a pattern could fit there
- Exception Handling
    - Ensure that each exception is raised and handled correctly
    - Ensure that you have a well-defined exception hierarchy
    - Split the exceptions in two types: technical and business

### Branching Strategy

### Application Structure

- Ensure that your changes are correctly written on layers and it respects the Spring Boo App Structure
- Do not mixt up a Rest Service with a Web App (like Spring Rest with Spring MVC )

### Model

- Understand the meaning of each model you defined and treat it like the most appropiate terminology for it: DTO (form
  for MVC), entity, Value Object, Java Bean
- Place it in the correct package

### Rest API

- Ensure your Rest API respects the REST maturity levels
- Error Codes
    - Ensure that in case of any error or exception the API replies with the standard error codes (defined at the system
      level)
    - Do not write Rest API which have different directions for receiving requestions from
        - Example: having a service which facilitates communication with an external 3rd party, do not expose the same
          service for the 3rd party to request back, for this use a different service (e.g. a notification service)
        - You can get into a confusion when you have to handle differently the same exception in the service, but it
          comes from different directions, you have 2 clients and cannot reply with the same error codes (one should be
          internally and the other one specific to the 3rd party)
- DTO
    - Use DTO pattern for passing data between controller and service layer (at least when using **sensitive** or **
      aggregated** data)

### MVC

- Ensure that your Model-View-Controller parts of the Web Application are compliant to the Best Practices
    - JSP don't have business logic (no Java code, only JSTL, Spring or Thymeleaf tags)
    - Model doesn't have business logic
    - Controller delegates the requests to the business (service) layer, it doesn't have logic
    - Use DTO (classes ending with Form in case of MVC) pattern for passing data between controller and service layer (
      at least when using **sensitive** or **aggregated** data)

### Performance

- Release resources (HTTP connections, DB connections, Files, any I/O streams )

### Security

### Thead-safety

- Ensure your code is not a candidate for race conditions and deadlocks

### Logging

### Alerting

# Code Quality

## Clean Code

Ensure that the code is clean as much as possible. Check also that SOLID principles are followed TODO Link to be
provided

## Design Patterns

Recommend a design pattern where is the case

## Naming Conventions

## App Structure

Check that the changes are correctly written on layers and it respects the Spring Boot App Structure Do not mixt up a
Rest Service with a Web App

## Model

Understand the meaning of usage of each model and try to find where is the most appropriate to be placed as TODO - link
to be provided

## Exception Handling

Ensure that each exception is raised and handled correctly 

## Unit Testing

Coverage of minimum 80% Ensure that all corner cases are covered and it follows the unit testing standards

## Rest API

Ensure that the API changes respect the REST maturity levels 

## Error Codes

Ensure that in case of a program error or exception, the API replies with the standard error codes

## MVC

Ensure that the Model-View-Controller parts of the Web Application are compliant with the Best Practices 


For more information:

1. [Best practices for REST API design](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/#h-name-collections-with-plural-nouns)
2. [REST: Good Practices for API Design](https://medium.com/hashmapinc/rest-good-practices-for-api-design-881439796dc9)



# Resolving a Production Issue on a Live Server


## Notify All Stakeholders

This can be done in form of a slack message to the general channel, an email copying relevant personnel or through any communication tool that the team uses. The importance of communication is to bring up the issue to everyone's attention and for all hands to be on deck. Sometimes, someone may just respond to your message with why the issue is happening (assuming it was a mistake from his/her part). But the goal is to inform and bring in the members of your team.


## Reproduce : Replicate the production environment locally

- Replicate locally and step through code to figure out what is going on.
- Add logs and replicate in production, then use logs to debug. This is only feasible if it is easy to do additional deployments that contain the logging code, and if the issue is in-fact reproducible.
- Write similar code to what’s running in production (often starting with a copy/pasted variant of the production code), and try to replicate and isolate the issue that way.

The objective here is to reproduce the exact same bug that exists in the production environment in a more accessible location. In the local environment, we can change data, slow down the execution, and write tons of logs without users being impacted in any way.


## Root Cause Analysis & Fix

Logging and debuggers are your best friends here. If you’re dealing with a large codebase or new to the project, just attach a debugger and follow through navigation and triggering actions. Else, add logs around the suspicious code and perform the steps. You’ll eventually find the piece of code that’s causing the issue.

## Re-test & Regression Testing
Test the steps that you found earlier, which caused the bug.

## Backup the System Before Implementing Complex Solution

## Document the Problem and How it was Resolved

add the problem and the steps you took towards resolving it to the engineering runbook. The importance of this, is that it will help the team to quickly recover from such when/if it happens next time. It also serves as a reference to the team when they want to rebuild the system to be resistant to such issues.







