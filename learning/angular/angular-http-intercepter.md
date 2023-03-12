---
description: >-
  Http Interceptor is an Angular middleware intercepting HTTP requests and
  responses globally. It allows users to modify or handle them before sending or
  receiving the data.
---

# \[Angular] Http Intercepter

## Common use cases of different HTTP interceptor

* HTTP Header Interceptor
* Formatting JSON Responses
* Error Handling

## Implementation

1. Create your component

{% code lineNumbers="true" %}
```typescript
import { HttpClient } from '@angular/common/http';
import { Component, OnInit } from '@angular/core';
import { catchError, of } from 'rxjs';

@Component({
  selector: 'app-root',
  template: '
    <div>App component works</div>
    <div>{{ data | json }}</div>',
  styleUrls: ['./app.component.css'],
})
export class AppComponent implements OnInit {
  data: any;
  constructor(private http: HttpClient) {}
  ngOnInit(): void {
    const apiUrl = 'https://jsonplaceholder.typicode.com/todos/1';
    const notFoundUrl = 'https://example.com/404';
    this.http
      .get(apiUrl)
      // .get(notFoundUrl)
      // the catchError is useful for handling error
      .pipe(catchError((err) => of("there's error")))
      .subscribe((data) => (this.data = data));
  }
  title = 'interceptor-demo';
}
```
{% endcode %}

2. Create your interceptor class implementing HttpInterceptor interface with `intercept()` method

```typescript

import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
} from '@angular/common/http';
import { Observable } from 'rxjs';

export class XXXInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    return next.handle(req)
  }
}

```

3. Add interceptor class to app.module.ts to make it globally accessible

```typescript

import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { XXXInterceptor } from './core/interceptor/XXX-interceptor';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, HttpClientModule],
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: XXXInterceptor,
      multi: true,
    },
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}

```

## HTTP Header Interceptor

{% code title="header-interceptor.ts" %}
```typescript
import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
} from '@angular/common/http';
import { Observable } from 'rxjs';

export class HeaderInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    const API_KEY = '123456';
    // passes the modified request to the next HttpHandler in the chain.
    return next.handle(req.clone({ setHeaders: { API_KEY } }));
  }
}

```
{% endcode %}

_Check the developer tool's Network tab, you will see the API\_KEY_

![](<../../.gitbook/assets/Screenshot 2023-03-12 at 4.45.05 PM.png>)



## Format Interceptor

```typescript
import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
  HttpResponse,
} from '@angular/common/http';
import { Injectable } from '@angular/core';
import { filter, map, Observable } from 'rxjs';

@Injectable()
export class FormatInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
  
  // The filter operator is used to only operate on HTTP responses containing 'todo' in the URL
    return next.handle(req).pipe(
      filter(
        (event) => event instanceof HttpResponse && req.url.includes('todo')
      ),

      map(
        (event) => {
          const httpEvent = event as HttpResponse<any>;
          // using destructive operator to get desired key
          const { userId, title } = httpEvent.body; 
          const cloneEvent = httpEvent.clone({
            body: {
              userId,
              title,
            },
          });

          return cloneEvent;
        }
      )
    );
  }
}

```

Check the rendering, you will see only userId and title being returned

![](<../../.gitbook/assets/Screenshot 2023-03-12 at 4.59.35 PM.png>)

### Error Handler

```typescript
import {
  HttpEvent,
  HttpHandler,
  HttpInterceptor,
  HttpRequest,
} from '@angular/common/http';
import { Observable, retry } from 'rxjs';

export class ErrorRetryInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
  // retry when error occurs
    return next.handle(req).pipe(retry(2));
  }
}

```

Comment line 19, and comment out line 20 in `app.component.ts` trying to request resource from Not found page, you will see request being retried triple times

![](<../../.gitbook/assets/Screenshot 2023-03-12 at 5.02.07 PM.png>)



### References

[intro-to-angular-http-interceptors](https://ultimatecourses.com/blog/intro-to-angular-http-interceptors)

