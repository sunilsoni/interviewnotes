RxJS
====

RxJS is a library for composing asynchronous and callback-based code in a functional, reactive style using Observables. Many APIs such as  HttpClient produce and consume RxJS Observables and also uses operators for processing observables.

For example, you can import observables and operators for using HttpClient,

```typescript
import { Observable, throwError } from 'rxjs';
import { catchError, retry } from 'rxjs/operators';
```


Utility functions provided by RxJS
-------------

The RxJS library also provides below utility functions for creating and working with observables.
1. Converting existing code for async operations into observables
2. Iterating through the values in a stream
3. Mapping values to different types
4. Filtering streams
5. Composing multiple streams


RxJS Operator
-------------
RxJS Operators are pure functions that transform information in the observable stream that create new observables, often based on the current observable.

The operators can be broken down in multiple categories. There are `creation operators` that create a new observable optionally from a source, such as a promise or a value, `Transformation operators` will transform the data in the stream, and `filtration operators` will act as a gate for the observable stream.

**Categories of operators**


|AREA          |OPERATORS         |
|--------------|------------------|
|Creation	     |from,fromEvent, of|
|Combination	 |combineLatest, concat, merge, startWith , withLatestFrom, zip|
|Filtering	   |debounceTime, distinctUntilChanged, filter, take, takeUntil|
|Transformation|bufferTime, concatMap, map, mergeMap, scan, switchMap|
|Utility	     |tap|
|Multicasting	 |share|

**1. Pipeable Operators [`pipe()`]**: These are operators that can be piped to existing Observables using the pipe syntax.
```typescript
class PostsComponent {

  private user: Observable<User>;

  ngOnInit() {
    this.posts = this.user.pipe(
      map(user => user.id),
      switchMap(id => 
        this.postsService.getPosts(id)
      )
    );
  }
}
```
**2. Map Operator [`map()`]**: The map() operator, basically, helps us to transform data using an observer. The map operator applies a given project function to each value emitted by the source Observable and emits the resulting values as an observable.
```typescript
import {map} from 'rxjs/operators';

const nums = of (1, 2, 3);

const mulValues = map ((val: number) => val * 2);
const mulNums = mulValues (nums);

mulNums.subscribe(x => console.log(x));

// Outputs
// 1
// 4
// 6
```
**3. Filter Operator [`filter()`]**: RxJS filter() is used to filter values emitted by source Observable on the basis of given predicate. If the condition returns true, filter will emit value obtained from source Observable otherwise not.

Example: Filter values for null
```typescript
this.countryName$ = this.filterDemoService.getCountry().pipe(
  filter(country => country.getCountryName() !== null),
  map(country => country.getCountryName()),
  catchError(err => {
	  console.error(err);
	  return of("");
  })
); 
```
**4. Concat Operator [`concat()`]**: Creates an output Observable which sequentially emits all values from given Observable and then moves on to the next.

Example: Concatenate a timer counting from 0 to 3 with a synchronous sequence from 1 to 10
```typescript
import { concat, interval, range } from 'rxjs';
import { take } from 'rxjs/operators';

const timer = interval(1000).pipe(take(4));
const sequence = range(1, 10);
const result = concat(timer, sequence);
result.subscribe(x => console.log(x));

// results in:
// 0 -1000ms-> 1 -1000ms-> 2 -1000ms-> 3 -immediate-> 1 ... 10
```
**5. FlatMap Operator [`flatMap()`] or mergeMap Operator [`mergeMap()`]**: flatMap() is an alias for mergeMap(). By using flatMap we can transform our event stream (the keypress events on the text field) into our response stream (the search results from the HTTP request).

Example: `app/services/search.service.ts`

```typescript
import {Http} from '@angular/http';
import {Injectable} from '@angular/core';

@Injectable()
export class SearchService {

  constructor(private http: Http) {}

  search(term: string) {
    return this.http
            .get('https://api.spotify.com/v1/search?q=' + term + '&type=artist')
            .map((response) => response.json())
  }
}
```
`app/app.component.ts`
```typescript
import { Component } from '@angular/core';
import { FormControl,
    FormGroup,
    FormBuilder } from '@angular/forms';
import { SearchService } from './services/search.service';
import 'rxjs/Rx';

@Component({
    selector: 'app-root',
    template: `
        <form [formGroup]="coolForm"><input formControlName="search" placeholder="Search Spotify artist"></form>

        <div *ngFor="let artist of result">
          {{artist.name}}
        </div>
    `
})
export class AppComponent {
    searchField: FormControl;
    coolForm: FormGroup;

    constructor(private searchService:SearchService, private fb:FormBuilder) {
        this.searchField = new FormControl();
        this.coolForm = fb.group({search: this.searchField});

        this.searchField.valueChanges
          .debounceTime(400)
            .flatMap(term => this.searchService.search(term))
            .subscribe((result) => {
                this.result = result.artists.items
            });
    }
}
```

**6. SwitchMap Operator [`switchMap()`]**: The switchMap() operator switches from one stream to another, unsubscribing from the previous observable and returning a new observable.
```typescript
import { Component } from '@angular/core';
import { FormControl, FormGroup, FormBuilder } from '@angular/forms';
import { SearchService } from './services/search.service';
import 'rxjs/Rx';

@Component({
    selector: 'app-root',
    template: `
        <form [formGroup]="coolForm"><input formControlName="search" placeholder="Search Spotify artist"></form>

        <div *ngFor="let artist of result">
          {{artist.name}}
        </div>
    `
})
export class AppComponent {
    searchField: FormControl;
    coolForm: FormGroup;

    constructor(private searchService:SearchService, private fb:FormBuilder) {
        this.searchField = new FormControl();
        this.coolForm = fb.group({search: this.searchField});

        this.searchField.valueChanges
          .debounceTime(400)
            .switchMap(term => this.searchService.search(term))
            .subscribe((result) => {
                this.result = result.artists.items
            });
    }
}
```

**7. Tap Operator [`tap()`]**: The `do()` operator was renamed to tap() in RxJS v5.5.x as part of the upgrade to lettable operators to avoid a confict with the reserved word do (part of the do-while loop).

RxJS Tap operator uses to perform a side effect for every emission on the source Observable but returns an Observable that is identical to the source.
```typescript
getProducts(): Observable<any[]> {
  return this.http.get<any[]>(apiUrl)
    .pipe(
      tap(product => console.log('fetched products')),
      catchError(this.handleError('getProducts', []))
    );
}
```

**8. Catch Operator [`catch()`]**: The catch() operator was renamed in RxJS v5.5.x to catchError(). The catchError() operator to receive any error notifications that are emitted in the observable stream.
```typescript
getProduct(id: number): Observable<any> {
  const url = `${apiUrl}/${id}`;
  return this.http.get<any>(url).pipe(
    tap(_ => console.log(`fetched product id=${id}`)),
    catchError(this.handleError<any>(`getProduct id=${id}`))
  );
}
```

**9. forkJoin Operator [`forkJoin()`]**: The forkJoin() operator is similar to the `Promise.all()` method in that it starts (forks) multiple observers at once and then joins the final values from each observable when all observables complete. It is important to note that if any of the input observables never complete, then the forkJoin() will never complete.

Example: Multiple http calls in parallel using forkJoin()
```
Observable.forkJoin(
    call1(params),
    call2(params),
    call3(params)
).subscribe((responses) => {
    // responses[0] -> response of call1
    // responses[1] -> response of call2
    // responses[2] -> response of call3
})
```

**10. retry Operator [`retry()`]**:  retry() operator returns source Observable with the exception of an error. When source Observable calls error then retry operator resubscribe it for the maximum of given number of time. If Observable starts emitting elements and suppose at any point it calls error before completion, then retry operator will resubscribe the source Observable and starts emitting from start again.
```typescript
return this.http
           .get(this.url)
           .retry(5);
```

**11. StartWith Operator [`startWith()`]**:
```typescript
import { startWith } from 'rxjs/operators';
import { of } from 'rxjs';

//emit (1,2,3)
const source = of(1, 2, 3);
//start with 0
const example = source.pipe(startWith(0));
//output: 0,1,2,3
const subscribe = example.subscribe(val => console.log(val));
```

**12. Of Operator [`of()`]**:
```typescript
import { of } from 'rxjs';
//emits any number of provided values in sequence
const source = of(1, 2, 3, 4, 5);
//output: 1,2,3,4,5
const subscribe = source.subscribe(val => console.log(val));
```

**13. take Operator [`take()`]**: take() an operator returns the first N values observed and complete stream. It is also another filteration operator.
```typescript
import { interval } from ‘rxjs’;
import { take } from ‘rxjs/operators’;

const intervalCount = interval(1000);
const takeFive = intervalCount.pipe(take(5));
takeFive.subscribe(x => console.log(x));
```
Output
```
0, 1, 2, 3, 4
```
The above example will take only the first five elements after every 5 seconds with the 1-second interval for five seconds.


What is subscribing?
-------------------


An Observable instance begins publishing values only when someone subscribes to it. So you need to subscribe by calling the **subscribe()** method of the instance, passing an observer object to receive the notifications.

```typescript
// Creates an observable sequence of 5 integers, starting from 1
const source = range(1, 5);

// Create observer object
const myObserver = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

// Execute with the observer object and Prints out each item
myObservable.subscribe(myObserver);
// => Observer got a next value: 1
// => Observer got a next value: 2
// => Observer got a next value: 3
// => Observer got a next value: 4
// => Observer got a next value: 5
// => Observer got a complete notification
```



Observable
------------ 

An Observable is a unique Object similar to a Promise that can help manage async code. Observables are not part of the JavaScript language so we need to rely on a popular Observable library called RxJS.
The observables are created using new keyword.
```typescript
import { Observable } from 'rxjs';

const observable = new Observable(observer => {
  setTimeout(() => {
    observer.next('Hello from a Observable!');
  }, 2000);
});
```


Observer
------------ 

Observer is an interface for a consumer of push-based notifications delivered by an Observable. It has below structure,
```typescript
interface Observer<T> {
  closed?: boolean;
  next: (value: T) => void;
  error: (err: any) => void;
  complete: () => void;
}
```
A handler that implements the Observer interface for receiving observable notifications will be passed as a parameter for observable as below,
```javascript
myObservable.subscribe(myObserver);
```
*Note: If you do not supply a handler for a notification type, the observer ignores notifications of that type.*


Error handling in observables
------------ 

We can handle errors by specifying an **error callback** on the observer instead of relying on try/catch which are ineffective in asynchronous environment. For example, you can define error callback as below,
```typescript
myObservable.subscribe({
  next(num) { console.log('Next num: ' + num)},
  error(err) { console.log('Received an errror: ' + err)}
});
```


Observable creation functions
------------ 

RxJS provides creation functions for the process of creating observables from things such as promises, events, timers and Ajax requests. Let us explain each of them with an example,

1. Create an observable from a promise

```typescript
import { from } from 'rxjs'; // from function
const data = from(fetch('/api/endpoint')); //Created from Promise
data.subscribe({
  next(response) { console.log(response); },
  error(err) { console.error('Error: ' + err); },
  complete() { console.log('Completed'); }
});
```
2. Create an observable that creates an AJAX request
```typescript
import { ajax } from 'rxjs/ajax'; // ajax function
const apiData = ajax('/api/data'); // Created from AJAX request
// Subscribe to create the request
apiData.subscribe(res => console.log(res.status, res.response));
```
3. Create an observable from a counter
```typescript
import { interval } from 'rxjs'; // interval function
const secondsCounter = interval(1000); // Created from Counter value
secondsCounter.subscribe(n =>
  console.log(`Counter value: ${n}`));
```
4. Create an observable from an event
```typescript
import { fromEvent } from 'rxjs';
const el = document.getElementById('custom-element');
const mouseMoves = fromEvent(el, 'mousemove');
const subscription = mouseMoves.subscribe((e: MouseEvent) => {
  console.log(`Coordnitaes of mouse pointer: ${e.clientX} * ${e.clientY}`);
  });
```


What will happen if you do not supply handler for observer?
------------ 

Normally an observer object can define any combination of next, error and complete notification type handlers. If you do not supply a handler for a notification type, the observer just ignores notifications of that type.

Promise vs Observable
------------ 

**Promises**:

* return a single value
* not cancellable
* more readable code with try/catch and async/await


**Observables**:

* work with multiple values over time
* cancellable
* support map, filter, reduce and similar operators
* use Reactive Extensions (RxJS)
* an array whose items arrive asynchronously over time

| Observable | Promise |
|---- | --------- |
| Declarative: Computation does not start until subscription so that they can be run whenever you need the result | Execute immediately on creation|
| Provide multiple values over time | Provide only one |
| Subscribe method is used for error handling which makes centralized and predictable error handling| Push errors to the child promises |
| Provides chaining and subscription to handle complex applications | Uses only .then() clause |


