# \[Angular] Angular version update

{% hint style="info" %}
**Angular 15 Update:**\
The prior versions of main.ts also contained a call to `enableProdMode();`. This is no longer needed, hence removed from Angular 15.
{% endhint %}

{% hint style="info" %}
**Angular 13 Update:**

Angular no longer supports for IE 11. Hence removes the differential loading from version 13.
{% endhint %}

{% hint style="info" %}
**Angular 12 Update:**&#x20;

ng build does a production build. In the prior versions of Angular, we needed to specify the flag `ng build --prod` for a production build. The production build optimizes, minimizes, and uglifies the code.\
\
You can use the `ng build --optimization=false` to stop the compiler from optimizing, minimizing, and uglifing the code.
{% endhint %}

{% hint style="info" %}
**Angular 7 Update:**

Since Angular 7, it had a new feature called [conditional polyfill loading (differential loading)](https://auth0.com/blog/angular-8-differential-loading/). Now Angular builds two versions of script files, one for es2015 (runtime-es2015.js, polyfills-es2015.js, vendor-es2015.js, main-es2015.js) & another for es5 (runtime-es5.js, polyfills-es5.js, vendor-es5.js, main-es5.js). The es2015 (es6) is for modern browsers, and es5 is for older browsers, which do not support the new features of es2015.
{% endhint %}

{% hint style="info" %}
**Angular 6 Update:**\
The The `angular-cli.json becomes angular.json`
{% endhint %}

{% hint style="info" %}
**Angular 2 Update:**&#x20;

Angular 2 generated only three script files (inline.js, styles.bundle.js & main.bundle.js)
{% endhint %}

