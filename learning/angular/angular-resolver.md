---
description: >-
  Angular resolver is a feature to resolve data before component is displayed.
  Once a resolver is bound to a specific path, Angular will  run the resolver's
  code and fetch the data before navigation
---

# \[Angular] Resolver

The main purpose of Angular resolver is to get data prepared before the route is navigated. By prefetching the data before navigating to the route, the user will experience faster load times and a smoother transition to the new content because you can still see previous page's content while waiting for new content.



Here's a resolver sample code&#x20;

{% code title="users.resolver.ts" %}
```typescript
import { Injectable } from '@angular/core';
import {
  Router,
  Resolve,
  RouterStateSnapshot,
  ActivatedRouteSnapshot,
} from '@angular/router';
import { Observable } from 'rxjs';
import { User } from './dto/user';
import { UsersService } from './users.service';
@Injectable({
  providedIn: 'root',
})
export class UsersResolver {
  constructor(private userService: UsersService) {}
  // automatically invoke the resolve method to pre-fetch data with service when routing to '/users'
  resolve(): Observable<User[]> {
    return this.userService.getUsers();
  }
}

```
{% endcode %}

The code is quite simple, the UsersResolver implement resolve function that invokes userService.getUsers() method to get data. Let's see what `userService` is responsible for

{% code title="users.service.ts" %}
```typescript

import { Injectable } from '@angular/core';
import { delay, EMPTY, empty, of, pipe } from 'rxjs';
import { User } from './dto/user';

@Injectable({
  providedIn: 'root',
})
export class UsersService {
  users: User[] = [
    { id: '1', name: 'Sam' },
    { id: '2', name: 'Andy' },
    { id: '3', name: 'David' },
  ];
  constructor() {}
  getUserById(id: string) {
    // in real application, it will call backend api to retrieve data
    // here we try to simulate this async operation by delaying for 1 second
    //emits users values in sequence
    const user = this.users.find((user) => user.id === id);

    return of(user).pipe(delay(1000));
  }
  getUsers() {
    // in real application, it will call backend api to retrieve data
    // here we try to simulate this async operation by delaying for 1 second

    //emits users values in sequence
    return of(this.users).pipe(delay(1000));
  }
}

```
{% endcode %}

the `getUsers` method mocks the I/O operation by delaying the request for 1 seconds amd then return data as Observable. Normally, it is an asynchronously 3rd-party or backend API call. With usersService being completed, we can bind the component data like this

{% code title="users.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-users',
  templateUrl: './users.component.html',
  styles: [],
})
export class UsersComponent implements OnInit {
  users: any[];
  constructor(private activatedRoute: ActivatedRoute) {}

  ngOnInit() {
    this.users = this.activatedRoute.snapshot.data['users'];
  }
}
```
{% endcode %}

we can retrieve data via the snapshot of activatedRoute service's. To access the service, remember to import `AppRoutingModule` in the app.module.ts. Last but not least, we need to provide the resolver in routing module:

```typescript

import { inject, NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { UsersResolver } from './users.resolver';
import { UsersComponent } from './features/users/users.component';

const routes: Routes = [
  {
    path: 'users',
    component: UsersComponent,
    resolve: { users: UsersResolver },
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

we register the name of resolver as `users` , that's the reason we get data by calling `this.activatedRoute.snapshot.data['users'];`&#x20;



To test your resolver, create your own user component, and inside you app.component.html, write a button for navigation, you can observe that the page staying at root page for 1 seconds, and then route to /`users` with content being rendered immediately

{% code title="app.component.html" %}
```html
<div *ngIf="title">Home page</div>
<a [routerLink]="['/users']"> Go to users page </a>
<router-outlet></router-outlet>

```
{% endcode %}

