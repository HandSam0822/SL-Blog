---
description: >-
  NgOptimizedImage is an Angular standalone directive to adopt performance best
  practices for loading images. It ensures the prioritization of LCP, which is
  an important metrics for web vitals
---

# \[Angular] Image Optimization

Since the official documentation is self-explanatory, this post aims to demonstrate the effect before and after introducing NgOptimzedImage. Here we have two image: `dog.jpg` and `cat.jpg`, and our component code is as following:&#x20;

```typescript

import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  template: `
    <h2>{{ title }}</h2>

    <img ngSrc="assets/cat.jpg" width="500" height="400" priority />
    <img ngSrc="assets/dog.jpg" width="300" height="200" />
  `,
  styles: [],
})
export class AppComponent {
  title = 'image-optimize-demo';
}
```

To compare the difference, we turn the network from **no throttling** to fast 3G, and the result is like this:

![cat image comes before dog image due to the priority setting](<../../.gitbook/assets/Screenshot 2023-03-09 at 4.08.17 PM.png>)![the dog image comes out hundrens ms after cat image](<../../.gitbook/assets/Screenshot 2023-03-09 at 4.08.18 PM.png>)



To inspect that the image is truly prioritized, you can go to the priority column in the network tab( if you can't find it, right click any of the column and you will see it)

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-09 at 4.18.30 PM.png" alt=""><figcaption><p>the request of cat.jpg get higher priority than dog.jpg</p></figcaption></figure>

### Warning

Angular displays a warning during development if&#x20;

* the LCP element is an image that does not have the `priority` attribute.
* the image will be visually distorted when rendered (the ratio of width and height)
* the`width` and `height` is set incorrectly

![example warning](<../../.gitbook/assets/Screenshot 2023-03-09 at 5.59.03 PM.png>)

\


### References

[Getting started with NgOptimizedImage](https://angular.io/guide/image-directive)

