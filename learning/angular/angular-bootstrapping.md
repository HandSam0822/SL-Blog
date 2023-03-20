---
description: >-
  It is commonly asked during the interview regarding the process of Angular
  bootstrap the application. Let's walk through it!
---

# \[Angular] Bootstrapping



### Bootstrapping in a nutshell:&#x20;

1. Running `ng serve`, it will compile the whole project step by step
2. Firstly, Angular will lookup the configuration file `angular.json`
3. In `angular.json`, we define the entry point at **main.ts** and **index.html** files.
4. In main.ts, the code looks like this

```typescript
// platformBrowserDynamic is the module responsible for loading the Angular application in the desktop browser
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
 
import { AppModule } from './app/app.module';
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
  
```

5. In main.ts, it specify AppModule as the root module, and so its metadata will be parsed

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
 
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
 
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }type
```

6. Angular will go through each properties and compile required modules
7. In the bootstrap array, it defines the component that angular should load when this Angular Module loads. Here we want `AppComponent` get bootstrapped when `AppModule` loads, hence we list it here.
8. Finally, we arrived at `AppComponent`, which is the root component of the `AppModule`. It also provides metadata inside `@Component` decorator, for example

```typescript
import { Component } from '@angular/core';
 
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'GettingStarted';
}
```

Angular will follow the template and style the metadata specify and render the view&#x20;



### Loads Angular & Third-party libraries & Application

[https://www.tektutorialshub.com/angular/angular-bootstrapping-application/#bootstrapping-in-angular](https://www.tektutorialshub.com/angular/angular-bootstrapping-application/#bootstrapping-in-angular)
