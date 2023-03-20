---
description: >-
  SCSS (Sassy CSS) is the preprocessor of CSS which provides more advance
  features than CSS to make code more reusable and maintainable. But it will
  still be compiled to CSS
---

# \[Style] CSS vs SCSS

### Variable

Define global variable to be used anywhere

```scss
$brand-color: #0074D9;
```

```scss
.header {
  background-color: $brand-color;
}

.btn {
  background-color: $brand-color;
  color: white;
}

```

### Function

```scss
// Define a function for calculating the width of a column in a grid system
@function column-width($total-columns, $gutter-width, $target-width) {
  $width: ($target-width / $total-columns) - ($gutter-width * 2);
  @return #{$width}px;
}

// Use the function to calculate the width of a column
.column {
  width: column-width(12, 20px, 960px);
}
```

### Mixin

we defined a mixin called `gradient-background` that takes two parameters, `$color1` and `$color2`. When this mixin is included in a selector using `@include`, it generates a `background` property with a linear gradient between the two colors.

```scss
// Define a mixin for adding a gradient background
@mixin gradient-background($color1, $color2) {
  background: linear-gradient(to bottom, $color1, $color2);
}

// Use the mixin in a selector
.header {
  @include gradient-background(#0074D9, #3D9970);
}

```

### Nest

Group related style for a button element

```scss
// Nest styles for a button element
.button {
  font-size: 1rem;
  padding: 10px 20px;
  
  &:hover {
    background-color: #0074D9;
    color: white;
  }
  
  &--primary {
    background-color: #0074D9;
    color: white;
  }
  
  &--secondary {
    background-color: #F0F0F0;
    color: #333;
  }
}

```



