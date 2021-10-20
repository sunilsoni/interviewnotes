

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

> The term idempotent is used more comprehensively to describe an operation that will produce the same results if executed once or multiple times [...] An idempotent function is one that has the property f(f(x)) = f(x) for any value x.


Ref: [4.2.2.  Idempotent Methods](https://www.rfc-editor.org/rfc/rfc7231#section-4.2.2)

## Safe Methods

Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.

This definition of safe methods does not prevent an implementation from including behavior that is potentially harmful, that is not entirely read-only, or that causes side effects while invoking a safe method. What is important, however, is that the client did not request that additional behavior and cannot be held accountable for it.

Of the request methods defined by this specification, the GET, HEAD, OPTIONS, and TRACE methods are defined to be safe

Ref: [4.2.1. Safe Methods](https://www.rfc-editor.org/rfc/rfc7231#section-4.2.1)

Ref: https://stackoverflow.com/questions/45016234/what-is-idempotency-in-http-methods


## Why DELETE method is defined as idempotent

Consider a client performs a `DELETE` request to delete a resource from the server. The server processes the request, the resource gets deleted and the server returns 204. Then the client repeats the same `DELETE` request and, as the resource has already been deleted, the server returns `404`.

Despite the different status code received by the client, the effect produced by a single `DELETE` request is the same effect of multiple `DELETE` requests to the same URI.

Finally, requests with idempotent methods can be repeated automatically if a communication failure occurs before the client is able to read the server's response. The client knows that repeating the request will have the same intended effect, even if the original request succeeded, though the response might be different.

## Why PATCH method is not idempotent

PATCH method, which is neither safe nor idempotent. However, to prevent collisions, PATCH requests can be issued such a way as to be idempotent, as quoted below:

A PATCH request can be issued in such a way as to be idempotent, which also helps prevent bad outcomes from collisions between two PATCH requests on the same resource in a similar time frame. Collisions from multiple PATCH requests may be more dangerous than PUT collisions because some patch formats need to operate from a known base-point or else they will corrupt the resource. Clients using this kind of patch application SHOULD use a conditional request such that the request will fail if the resource has been updated since the client last accessed the resource. For example, the client can use a strong ETag in an If-Match header on the PATCH request.


## When to Use Put and When Patch

When a client needs to replace an existing Resource entirely, they can use PUT. When they're doing a partial update, they can use HTTP PATCH.

For instance, when updating a single field of the Resource, sending the complete Resource representation can be cumbersome and uses a lot of unnecessary bandwidth. In such cases, the semantics of PATCH make a lot more sense.

Another important aspect to consider here is idempotence. PUT is idempotent; PATCH can be idempotent but isn't required to be. So, depending on the semantics of the operation we're implementing, we can also choose one or the other based on this characteristic.


Ref: https://www.baeldung.com/http-put-patch-difference-spring

## Why is PUT idempotent?

In  RFC 2616 citation, PUT is considered idempotent. When you PUT a resource, these two assumptions are in play:

1. You are referring to an entity, not to a collection.
2. The entity you are supplying is complete (the entire entity).

Let's look at one of your examples.

```json
{ "username": "skwee357", "email": "skwee357@domain.com" }
```

If you POST this document to `/users`, as you suggest, then you might get back an entity such as

```json
## /users/1

{
    "username": "skwee357",
    "email": "skwee357@domain.com"
}
 ```

If you want to modify this entity later, you choose between PUT and PATCH. A `PUT` might look like this:
```json
PUT /users/1
{
    "username": "skwee357",
    "email": "skwee357@gmail.com"       // new email address
}
 ```
You can accomplish the same using `PATCH`. That might look like this:


```json
PATCH /users/1
{
    "email": "skwee357@gmail.com"       // new email address
}

 ```
Here The `PUT` included all of the parameters on this user, but `PATCH` only included the one that was being modified (email).

When using PUT, it is assumed that you are sending the complete entity, and that complete entity replaces any existing entity at that URI. In the above example, the PUT and PATCH accomplish the same goal: they both change this user's email address. But PUT handles it by replacing the entire entity, while PATCH only updates the fields that were supplied, leaving the others alone.

Since PUT requests include the entire entity, if you issue the same request repeatedly, it should always have the same outcome (the data you sent is now the entire data of the entity). Therefore PUT is idempotent.

Ref: https://stackoverflow.com/questions/28459418/use-of-put-vs-patch-methods-in-rest-api-real-life-scenarios









