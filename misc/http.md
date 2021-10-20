

# HTTP methods overview



| Method      |      Scope   | Semantics | Idempotent | Safe |
|-----------------|------- --------|------------|------------|-----|
|  GET       |  collection     | Retrieve all resources in a collection| Yes | Yes |
|   GET     | collection     | Retrieve a single resource  |  Yes |Yes|
|  HEAD      | collection     | Retrieve all resources in a collection (header only)   | Yes |Yes |
|  HEAD      |  resource    | Retrieve a single resource (header only)  | Yes |  Yes|
| POST       |    collection  | Create a new resource in a collection  | No | No  |
|  PUT      |   resource   | Update a resource  |Yes | No  |
|   PATCH     |   resource   | Update a resource  | No | No |
|   DELETE     |  resource    | Delete a resource  |Yes | No |
|  OPTIONS      | any     | Return available HTTP methods and other options   | Yes | Yes |