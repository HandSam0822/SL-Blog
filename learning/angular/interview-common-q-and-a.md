---
description: >-
  The collections of common questions asked during the interview regarding web
  development or Angular
---

# \[Interview] Common Q\&A

1. What is the Ivy rendering engine and benefits of using it?
   1. Better Debugging: clearer error message
   2. Smaller Bundle Size: Tree shaking, Dead code elimination
   3. Improve Performance: AOT > JIT
2. How to upgrade a Angular 7 project to Angular 8? What are the challenges you might encounter?
   1. Using `ng update` command to update @angular/cli, @angular/code or any other dependencies to their latest version
   2. The challenges includes **compatibility issues with third-party libraries that may not be updated**; **API changes that may require code modification; changes to the syntax that leads to errors in the code**
3. How do you debug an Angular 8 project? Most commonly used techniques and debugging tools?
   1. Visual Studio Debugger: Allows you to set breakpoints on code execution
   2. Chrome Devtool
   3. Augury: Chrome extension to visualize component tree and inspect component properties&#x20;
4. What's HTML?
   1. Define structure and content of the web page
   2. It uses a set of tags to define various elements such as headings, paragraphs, lists, links, images, forms, and more.
5. What is **ngRx**?
   1. State Management library; centralized data storage; single source of truth;&#x20;
   2. Follow Flux pattern; data flow is unidirectional&#x20;
   3. Essential elements includes:&#x20;
      1. Store: Store the data that is globally accessible
      2. Action: The action to manipulate data
      3. Selector: Allow Component to desired data from Store
      4. Dispatcher: Dispatch action to Reducer and let Reducer do the rest of thing
      5. Reducer: Receive different kind of actions, and modify the data accordingly
6. What is **rxjs**
   1. Libraries to simplify and improve the reactive programming&#x20;
   2. Using Observable to more easily handle asynchronous code comparing to Callbacks and Promises.
   3. Provide a rich set of operators that can be used to transform the data stream and handle complex scenario such as throttling, debouncing, and error retry.
   4. It is often used in conjunction with Angular framework
7.  Typescript vs Javascript

    TS is the superset of JS, but provides many benefits over plain Javascript, especially for larger, more complex projects. But it ultimately will be transpiled to javascript code in production.

    1. Static Typing : Add static types to variables, functions, class properties. It can then catch type related errors in compile time rather than runtime.



8.  How nodejs do authentication?&#x20;

    There're mainly two type to authentication. Token based and session based

    For token-based, you can either use _JSON Web Token (JWT)_, t_hird-party library such as Passport.js_, or _OAuth 2.0 such as Google, Facebook, Github_, ...



    OAuth2.0: Resource owner, Client, Authorization server, Resource server

    Difference between OAuth1.0 and 2.0

    OAuth 2.0 is a more modern way to do authentication because

    1. Less complexity: OAuth2.0 use SSL/TLS encryption while OAuth 1.0 requires the use of cryptographic signatures
    2. Token expiration: OAuth1.0's token never expired, while OAuth 2.0 provides a more secure way by revoking the token after a period of time



    OAuth 2.0 Step

    1. Client (Your Web app) **redirect** users to auth server requesting authorization
    2. The auth server prompts users to **grant permission** for client to access their data&#x20;
    3. The auth server **issues an access token** to the client
    4. The client uses the access token to access the  user's data on the resource server
9. Common technique to improve the performance of Angular application
   1. Lazy Loading: Only Load data when user navigate to the route
   2. Server Side rendering: Reduce browser's download size
   3. Change Detection Strategy: onPush makes it activated only when ref change
   4. Tree Shaking: Decrease the Bundle size by getting rid of dead code
   5. AOT compilation: Template is precompile, so browser don't need to do it
   6. Caching: Reduce the amount of time app spends fetching data from the servers
10. What is a closure

    Closure is usually used to create private variables and functions, implementing callbacks, and creating factories.

    Closure Example:&#x20;

```typescript
function outerFunction() {
  var outerVariable = 10;

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

var closure = outerFunction();
closure(); // Output: 10

```

11. What is Web workers?

    Web Worker is a Javascript feature allowing for **multi-threading** in web applications. It is essentially a separate JavaScript file running in a background thread, separate from the main UI thread. This allows the web application to **perform time-consuming tasks** without blocking the user interface or causing the web page to become unresponsive.
12. What is pagination

    Pagination is the process of dividing a large set of data into smaller, more manageable chunks, for easier viewing and navigation. It is a common technique used in web design to present large amounts of data to users in a more organized and user-friendly way.

    \
