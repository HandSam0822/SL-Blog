---
description: >-
  Caching webpage allows users to not waiting for response under slow network
  environment. We can use Observable and local storage to serve a locally cached
  version at initial stage and update later
---

# \[Angular] Http Fast Caching

### Use case&#x20;

We want to make a Http server request (in this case, apiUrl = https://api.github.com/search/repositories?q=angular), getting the response and rendering on `app.component.html`

To test the behaviour before and after introducing cache mechanism, you can open the developer tools's network tab, and switch from no-throttle to slow3G. Before caching the webpage, you can observe that the page is left blank for a long time each time you refresh the page. The reason behind it is that we need to make an API call and wait until the response is resolved.&#x20;

Here we introduce the cache solution, and give observable an initial value before fetching real data. &#x20;

{% code title="app.component.ts" %}
```typescript

import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { map, startWith } from 'rxjs';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent implements OnInit {
  repos$: any;
  constructor(private http: HttpClient) {}
  ngOnInit() {
    const apiUrl = 'https://api.github.com/search/repositories?q=angular';
    const CACHE_KEY = 'cache_key';

    // you still need to make a http call, but the startWith operator ensuring
    // that the component displays some data while the HTTP request is in progres
    this.repos$ = this.http.get<any>(apiUrl).pipe(map((data) => data.items));

    // as this.repos receive response from API, it will refresh data store in cache key
    this.repos$.subscribe((response: any) => {
      localStorage.setItem(CACHE_KEY, JSON.stringify(response));
    });

    // the startWith operator will provide an initial value to the repos observable,
    // either the cached data from localStorage or an empty array,
    this.repos$ = this.repos$.pipe(
      startWith(JSON.parse(localStorage[CACHE_KEY]) || '[]')
    );
  }
}

```
{% endcode %}

The logic of view is quiet simple, iterating the repos and displaying its attributes

{% code title="app.component.html" %}
```html
<h1>Angular fast caching</h1>
<div *ngFor="let repo of repos$ | async">
  <h3>{{ repo.name }}</h3>
  <div>{{ repo | json }}</div>
</div>
```
{% endcode %}



### References

[Fast HTTP Caching With Angular HTTP Observables](https://www.youtube.com/watch?v=Yf1FfhMetjs)

