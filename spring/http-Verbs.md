HTTP Verbs
==========


GET
----
The GET method is designed to request a specific resource. In essence, it literally “gets” the resource in question, and is pretty limited to just that action. GET requests should only retrieve data, leaving other methods to perform the other transformative actions.



POST
----
POST affects the related resources attached to a targeted resource. POST allows an API to submit an attribute or entity to a given resource; in practice, this means the targeted resource receives a subordinate resource that is part of a larger collection

PUT
----
PUT is somewhat the polar opposite of GET. While GET requests a specific resource, PUT places that resource in the remote directory. It should be noted that PUT assumes either the resource does not exist or the resource is fine to be overwritten – when using PUT, all representations of the target resource will be replaced by the payload.


DELETE
----
DELETE is the most clear-cut method on this list because it does exactly what’s on the tin – DELETE deletes a targeted resource. The typical response for a deletion method is simply to reply with an “OK” status – either the resource was deleted, or it was not.

PATCH
----
PATCH is designed to partially modify a targeted resource. In other words, while PUT places a resource in the target service, PATCH modifies that resource, as opposed to replacing it. This is a good way to update files or versions.

OPTIONS
----
The OPTIONS method changes the different communication options held by the target resource. This can be used to both open up more channels of communication and lock them down – for this reason, the OPTIONS method should be considered akin to a faucet which can be opened and closed with relative granularity.

HEAD
----
HEAD is an interesting method in that it mirrors some functionality of another METHOD while unlocking additional possibilities. HEAD requests a GET response from a given resource, but with the response body excised. While that may seem overly simplistic, it allows greater flexibility and power for other API extensions – for instance, you can pass the headers of a resource to another request in an attempt to mimic a different requesting environment or situation, which is extremely helpful for testing and troubleshooting.






