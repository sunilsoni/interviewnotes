Good Practices
=============


Good Practices for REST API Design
-----------------------------------

A REST API is an application programming interface that conforms to specific architectural constraints, like stateless communication and cacheable data. It is not a protocol or standard. While REST APIs can be accessed through a number of communication protocols, most commonly, they are called over HTTPS,


Accept and respond with JSON
----------------------------
REST APIs should accept JSON for request payload and also send responses to JSON. JSON is the standard for transferring data. Almost every networked technology can use it

To make sure that when our REST API app responds with JSON that clients interpret it as such, we should set `Content-Type` in the response header to `application/json`

Use nouns instead of verbs in endpoint paths
-----------------------------------
We shouldn’t use verbs in our endpoint paths. Instead, we should use the nouns which represent the entity that the endpoint that we’re retrieving or manipulating as the pathname.

we should create routes like 
- GET /articles/ for getting news articles. Likewise, 
- POST /articles/ is for adding a new article , 
- PUT /articles/:id is for updating the article with the given id. 
- DELETE /articles/:id is for deleting an existing article with the given ID.

Nesting resources for hierarchical objects
-----------------------------------
When designing endpoints, it makes sense to group those that contain associated information. That is, if one object can contain another object, you should design the endpoint to reflect that.

For example, if we want an endpoint to get the comments for a news article, we should append the /comments path to the end of the /articles path.


Handle errors gracefully and return standard error codes
-----------------------------------
we should handle errors gracefully and return HTTP response codes that indicate what kind of error occurred. This gives maintainers of the API enough information to understand the problem that’s occurred. We don’t want errors to bring down our system, so we can leave them unhandled, which means that the API consumer has to handle them.

Common error HTTP status codes include:

- **400 Bad Request** – This means that client-side input fails validation.
- **401 Unauthorized** – This means the user isn’t not authorized to access a resource. It usually returns when the user isn’t authenticated.
- **403 Forbidden** – This means the user is authenticated, but it’s not allowed to access a resource.
- **404 Not Found** – This indicates that a resource is not found.
- **500 Internal server error** – This is a generic server error. It probably shouldn’t be thrown explicitly.
- **502 Bad Gateway** – This indicates an invalid response from an upstream server.
- **503 Service Unavailable** – This indicates that something unexpected happened on server side (It can be anything like server overload, some parts of the system failed, etc.).

We should be throwing errors that correspond to the problem that our app has encountered. For example, if we want to reject the data from the request payload, then we should return a 400 response


Allow filtering, sorting, and pagination
-----------------------------------
The databases behind a REST API can get very large. Sometimes, there’s so much data that it shouldn’t be returned all at once because it’s way too slow or will bring down our systems. Therefore, we need ways to filter items.

We also need ways to paginate data so that we only return a few results at a time. We don’t want to tie up resources for too long by trying to get all the requested data at once.

Filtering and pagination both increase performance by reducing the usage of server resources. As more data accumulates in the database, the more important these features become.


Maintain Good Security Practices
-----------------------------------

Most communication between client and server should be private since we often send and receive private information. Therefore, using SSL/TLS for security is a must.

People shouldn’t be able to access more information that they requested. For example, a normal user shouldn’t be able to access information of another user. They also shouldn’t be able to access data of admins.

If we choose to group users into a few roles, then the roles should have the permissions that cover all they need and no more.

Cache data to improve performance
-----------------------------------
We can add caching to return data from the local memory cache instead of querying the database to get the data every time we want to retrieve some data that users request. The good thing about caching is that users can get data faster. However, the data that users get may be outdated. This may also lead to issues when debugging in production environments when something goes wrong as we keep seeing old data.

There are many kinds of caching solutions like Redis, in-memory caching,etc. We can change the way data is cached as our needs change.

Versioning our APIs
--------------------

We should have different versions of API if we’re making any changes to them that may break clients. The versioning can be done according to semantic version (for example, 2.0.6 to indicate major version 2 and the sixth patch) like most apps do nowadays.

Versioning is usually done with /v1/, /v2/, etc. added at the start of the API path.






