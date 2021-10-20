

# HTTP methods overview



| Method      |      Scope   | Semantics | Idempotent | Safe |
|-----------------|---------------|------------|------------|-----|
|  GET       |  collection     | Retrieve all resources in a collection| Yes | Yes |
|   GET     | collection     | Retrieve a single resource  |  Yes |Yes|
|  HEAD      | collection     | Retrieve all resources in a collection (header only)   | Yes |Yes |
|  HEAD      |  resource    | Retrieve a single resource (header only)  | Yes |  Yes|
| POST       |    collection  | Create a new resource in a collection  | No | No  |
|  PUT      |   resource   | Update a resource  |Yes | No  |
|   PATCH     |   resource   | Update a resource  | No | No |
|   DELETE     |  resource    | Delete a resource  |Yes | No |
|  OPTIONS      | any     | Return available HTTP methods and other options   | Yes | Yes |



## Idempotency in HTTP

Idempotency is a property of HTTP methods.

A request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request. Of the request methods defined by this specification, PUT, DELETE, and safe request methods are idempotent.  

Like the definition of safe, the idempotent property only applies to what has been requested by the user; a server is free to log each request separately, retain a revision control history, or implement other non-idempotent side effects for each idempotent request.  

Ref: [4.2.2.  Idempotent Methods](https://www.rfc-editor.org/rfc/rfc7231#section-4.2.2)

## Why DELETE method is defined as idempotent

Consider a client performs a `DELETE` request to delete a resource from the server. The server processes the request, the resource gets deleted and the server returns 204. Then the client repeats the same `DELETE` request and, as the resource has already been deleted, the server returns `404`.

Despite the different status code received by the client, the effect produced by a single `DELETE` request is the same effect of multiple `DELETE` requests to the same URI.

Finally, requests with idempotent methods can be repeated automatically if a communication failure occurs before the client is able to read the server's response. The client knows that repeating the request will have the same intended effect, even if the original request succeeded, though the response might be different.

## Why PATCH method is not idempotent

PATCH method, which is neither safe nor idempotent. However, to prevent collisions, PATCH requests can be issued such a way as to be idempotent, as quoted below:

A PATCH request can be issued in such a way as to be idempotent, which also helps prevent bad outcomes from collisions between two PATCH requests on the same resource in a similar time frame. Collisions from multiple PATCH requests may be more dangerous than PUT collisions because some patch formats need to operate from a known base-point or else they will corrupt the resource. Clients using this kind of patch application SHOULD use a conditional request such that the request will fail if the resource has been updated since the client last accessed the resource. For example, the client can use a strong ETag in an If-Match header on the PATCH request.

## Safe Methods

Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource. 

This definition of safe methods does not prevent an implementation from including behavior that is potentially harmful, that is not entirely read-only, or that causes side effects while invoking a safe method. What is important, however, is that the client did not request that additional behavior and cannot be held accountable for it.  

Of the request methods defined by this specification, the GET, HEAD, OPTIONS, and TRACE methods are defined to be safe

Ref: [4.2.1. Safe Methods](https://www.rfc-editor.org/rfc/rfc7231#section-4.2.1)

Ref: https://stackoverflow.com/questions/45016234/what-is-idempotency-in-http-methods








