
# Angular Services

Angular services are singleton objects which get instantiated only once during the lifetime of an application. It contains method that maintain data throughout the life of an application, i.e. data does not get refreshed and is available all the time. The main objective of a service is to organize and share business logic, models, or data and functions with different components of an Angular application.

**Benefits**

An Angular service is a stateless object and provides some very useful functions. These functions can be invoked from any component of Angular, like Controllers, Directives, etc. This helps in dividing the web application into small, different logical units which can be reused.

```typescript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable({ // The Injectable decorator is required for dependency injection to work
    // providedIn option registers the service with a specific NgModule
    providedIn: 'root',  // This declares the service with the root app (AppModule)
})
export class RepoService {
    constructor(private http: Http) { }

    fetchAll() {
       return this.http.get('https://api.github.com/repositories');
    }
}
```

The above service uses Http service as a dependency.



















For more information:

[Introduction to services and dependency injection](https://angular.io/guide/architecture-services)