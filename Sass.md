# Q1: What is Sass?
- Sass is a stylesheet language that's compiled to CSS.
# Q2: Why Sass?
- Stylesheets are becoming large, more complex, and harder to maintain.
# Q3: What dose sass offer?
- Preprocessing
- Variables
- Nesting
- Break it down
- Modules
- Mixins
- Extend/Inheritance
- Operators
# Q4: What dose the syntax look like?
- Statment
	- Universal Statements
		- Variable declarations `$var: value`.
		- Flow control at-rules: `@if`,`@each`.
		- `@error`,`@warn`,`@debug`.
	- Css Statements
		- Style rules like `h1 {}`.
		- CSS at-rules like `@media`,`@font-face`.
		- Mixin uses using `@include`.
		- Function definitions using `@function`.
	- Top-Level Statements
		- Module loads using `@use`.
		- Imports using `@import`.
		- Mixin definitions using `@mixin`.
		- Function definitions using `@function`.
	- Other Statements
		- Property declarations.
		- The `@extend` rule may only be used within style rules.
- Expressions: An _expression_ is anything that goes on the right-hand side of a property or variable declaration.
	- Literals
		- Numbers
		- Strings
		- Colors
		- Boolean
		- null
		- List of values like `1.5em 1em 0 2em`, `Helvetica, Arial, sans-serif`, or `[col1-start]`.
		- Maps like `("background": red, "foreground": pink)`.
	- Operations
		- `==` and `!=`are used to check if two values are the same.
		- `+`, `-`, `*`, `/`, and `%` have their usual mathematical meaning for numbers, with special behaviors for units that matches the use of units in scientific math.
		- `<`, `<=`, `>`, and `>=` check whether two numbers are greater or less than one another.
		- `and`, `or`, and `not` have the usual boolean behavior. Sass considers every value "true" except for `false` and `null`.
		- `+`, `-`, and `/` can be used to concatenate strings.
		- `(` and `)` can be used to explicitly control the precedence order of operations.
	- Other Expressions
		- Variables, like `$var`.
		- Function calls, like `nth($list, 1)` or `var(--main-bg-color)`
		- Special functions, like `calc(1px + 100%)` or `url(http://myapp.com/assets/logo.png)`
		- The parent selector, `&`.
		- The value `!important`.

 
# Q5: What are special functions?

- url
- element
- progid
- expression

```sass
$roboto-font-path: "../fonts/roboto"

@font-face
    src: url("#{$roboto-font-path}/Roboto-Thin.woff2") format("woff2")
    font-family: "Roboto"
    font-weight: 100

@font-face
    src: url($roboto-font-path + "/Roboto-Light.woff2") format("woff2")
    font-family: "Roboto"
    font-weight: 300


@font-face
    src: url(#{$roboto-font-path}/Roboto-Regular.woff2) format("woff2")
    font-family: "Roboto"
    font-weight: 400
```

# Q6: What  rules do styles have?

##  Property Declarations
### Interpolation

```scss
// how to use interpolation?
@mixin prefix($property, $value, $prefixes) {
  @each $prefix in $prefixes {
    -#{$prefix}-#{$property}: $value;
  }
  #{$property}: $value;
}
// how to use the function?
.gray {
  @include prefix(filter, grayscale(50%), moz webkit);
}
// after compiling to css......
.gray {
  -moz-filter: grayscale(50%);
  -webkit-filter: grayscale(50%);
  filter: grayscale(50%);
}
```
### Nesting

```scss
.enlarge {
  font-size: 14px;
// how to nest with the same prefix?
  transition: {
    property: font-size;
    duration: 4s;
    delay: 2s;
  }

  &:hover { font-size: 36px; }
}

// after compiling to css......
.enlarge {
  font-size: 14px;
  transition-property: font-size;
  transition-duration: 4s;
  transition-delay: 2s;
}
.enlarge:hover {
  font-size: 36px;
}
```
### Hidden Declarations

```scss
$rounded-corners: false;

.button {
  border: 1px solid black;
  border-radius: if($rounded-corners, 5px, null);
}
```
### Meta meta.inspect
- You can use the `meta.inspect()`  to preserve the quotes.
```sass
@use "sass:meta"

$font-family-sans-serif: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto
$font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas

:root
  --font-family-sans-serif: #{meta.inspect($font-family-sans-serif)}
  --font-family-monospace: #{meta.inspect($font-family-monospace)}
```
## Parent Selector

#### Simple

```scss
.alert {
  &:hover { }
  [dir=rtl] & { }
  :not(&) { }
}

// after compiling to css......
.alert:hover { }
[dir=rtl] .alert { }
:not(.alert) { }
```
#### Adding Suffixes

```scss
.accordion {
  &__copy {
    &--open { }
  }
}
// after compiling to css
.accordion { }
.accordion__copy { }
.accordion__copy--open { }
```
#### In SassScript

```scss
.main aside:hover,
.sidebar p {
  parent-selector: &;
}
// after compiling to css
.main aside:hover,
.sidebar p {
  parent-selector: .main aside:hover, .sidebar p;
}
```

```scss
@mixin app-background($color) {
  #{if(&, '&.app-background', '.app-background')} { }
}

@include app-background(#036);

.sidebar {
  @include app-background(#c6538c);
}
```
####  Advanced Nesting

- `&` can be used as a SassScript expression, passed to functions, or used for interpolation. 

- Combined with selector functions and the `@at-root` rule, it enables powerful selector nesting.

- You can use the `selector.unify()` function to merge `&` with other selectors.

```scss
@use "sass:selector";
@mixin unify-parent($child){
	@at-root #{selector.unify(&,$child)}{
		@content
	}
}

.wrapper .field {
  @include unify-parent("input") {
  }
  @include unify-parent("select") {
  }
}

// after compiling to css
.wrapper input.field { }
.wrapper select.field { }
```
## Placeholder Selectos

```scss
%toolbelt {
  box-sizing: border-box;
  border-top: 1px rgba(#000, .12) solid;
  padding: 16px 0;
  width: 100%;

  &:hover { border: 2px rgba(#000, .5) solid; }
}

.action-buttons {
  @extend %toolbelt;
  color: #4285f4;
}

.reset-buttons {
  @extend %toolbelt;
  color: #cddc39;
}

// after compiling to css
.reset-buttons, .action-buttons {
  box-sizing: border-box;
  border-top: 1px rgba(0, 0, 0, 0.12) solid;
  padding: 16px 0;
  width: 100%;
}
.reset-buttons:hover, .action-buttons:hover {
  border: 2px rgba(0, 0, 0, 0.5) solid;
}

.action-buttons {
  color: #4285f4;
}

.reset-buttons {
  color: #cddc39;
}
```
# Q7: What are variables and their characteristics?

## Default Values

- Assign a value to a name that begins with `$`.
- Refer to that name instead of the value itself.

```scss
$base-color: #c6538c;
$border-dark: rgba($base-color, 0.88);

.alert {
  border: 1px solid $border-dark;
}
// after compiling to css
.alert {
  border: 1px solid rgba(198, 83, 140, 0.88);
}
```

- Variables with `!default` can be configured via the `@use` rule, commonly allowing customization in Sass libraries.

```scss
// _library.scss
$black: #000 !default;
$border-radius: 0.25rem !default;
$box-shadow: 0 0.5rem 1rem rgba($black, 0.15) !default;

code {
  border-radius: $border-radius;
  box-shadow: $box-shadow;
}

// style.scss
@use 'library' with (
  $black: #222,
  $border-radius: 0.1rem
);
```
## Built-in Variables 

- Variables that are defined by a built-in module cannot be modified.

```scss
@use "sass:math" as math;

// This assignment will fail.
math.$pi: 0;
```
## Scope

- Top-level variables are global, while block-scoped ones are local and only accessible within.

```scss
$global-variable: global value;

.content {
  $local-variable: local value;
  global: $global-variable;
  local: $local-variable;
}

.sidebar {
  global: $global-variable;

  // This would fail, because $local-variable isn't in scope:
  // local: $local-variable;
}
```

 ## Shadowing
 
- global & local

```scss
$variable: global value;

.content {
  $variable: local value;
  value: $variable;
}

.sidebar {
  value: $variable;
}
```
## Flow Control Scope

```scss
$dark-theme: true !default;
$primary-color: #f8bbd0 !default;
$accent-color: #6a1b9a !default;

@if $dark-theme {
  $primary-color: darken($primary-color, 60%);
  $accent-color: lighten($accent-color, 60%);
}

.button {
  background-color: $primary-color;
  border: 1px solid $accent-color;
  border-radius: 3px;
}
```
## Advanced Variable Functions

```scss
@use "sass:map";

$theme-colors: (
  "success": #28a745,
  "info": #17a2b8,
  "warning": #ffc107,
);

.alert {
  // Instead of $theme-color-#{warning}
  background-color: map.get($theme-colors, "warning");
}
```
# Q8: What functionalities do At-Rules include?

- @use
- @forward
- @import
- @mixin
- @function
- @extend
- @at-root
- @error
- @warn
- @debug
- @if,@each,@for,@while
### @use & @import & @forward

-  `@use` can't import that private member by starting its name with either `-` or `_`  .

```scss
@use "src/corners";
@use "src/corners" as c;
@use "src/corners" as *;

// override the variables’ default values!
@use 'library' with (
  $black: #222,
  $border-radius: 0.1rem
);
```

- with mixin

```scss
// source
$-black: #000;
$-border-radius: 0.25rem;
$-box-shadow: null;
@mixin styles {
  code { }
}
@use 'library';
// use
@include library.configure(
  $black: #222,
  $border-radius: 0.1rem
);
@include library.styles;
```

- Reassigning Variables

```scss
@use 'library';
library.$color: blue;
```

- Use `@use` for including files with namespacing and avoiding conflicts.
- Use `@forward` for re-exporting contents to other files.
- Avoid `@import` in modern Sass projects, as it's outdated and can lead to conflicts and performance issues.
## @mixin and @include

- Mixins allow you to define styles that can be re-used throughout your stylesheet.

```scss
@mixin reset-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

@mixin horizontal-list {
  @include reset-list;

  li {
    display: inline-block;
    margin: {
      left: -2px;
      right: 2em;
    }
  }
}
```

-  Arguments

```scss
@mixin rtl($property, $ltr-value, $rtl-value) {
  #{$property}: $ltr-value;

  [dir=rtl] & {
    #{$property}: $rtl-value;
  }
}

.sidebar {
  @include rtl(float, left, right);
}
```

-  Optional Arguments

```scss
@mixin replace-text($image, $x: 50%, $y: 50%) {
  text-indent: -99999em;
  overflow: hidden;
  text-align: left;

  background: {
    image: $image;
    repeat: no-repeat;
    position: $x $y;
  }
}

.mail-icon {
  @include replace-text(url("/images/mail.svg"), 0);
}
```

- Keyword Arguments

```scss
@mixin square($size, $radius: 0) {
  width: $size;
  height: $size;

  @if $radius != 0 {
    border-radius: $radius;
  }
}

.avatar {
  @include square(100px, $radius: 4px);
}
```

```scss
@mixin order($height, $selectors...) {
  @for $i from 0 to length($selectors) {
    #{nth($selectors, $i + 1)} {
      position: absolute;
      height: $height;
      margin-top: $i * $height;
    }
  }
}

@include order(150px, "input.name", "input.address", "input.zip");
```

-  Taking Arbitrary Keyword Arguments

```scss
@use "sass:meta";

@mixin syntax-colors($args...) {
  @debug meta.keywords($args);

  @each $name, $color in meta.keywords($args) {
    pre span.stx-#{$name} {
      color: $color;
    }
  }
}

@include syntax-colors(
  $string: #080,
  $comment: #800,
  $variable: #60b,
)
```

-  Content Blocks

```scss
@mixin hover {
  &:not([disabled]):hover {
    @content;
  }
}

.button {
  border: 1px solid black;
  @include hover {
    border-width: 2px;
  }
}
```

- Passing Arguments to Content Blocks

```scss
@mixin media($types...) {
  @each $type in $types {
    @media #{$type} {
      @content($type);
    }
  }
}

@include media(screen, print) using ($type) {
  h1 {
    font-size: 40px;
    @if $type == print {
      font-family: Calluna;
    }
  }
}
```
## @function

```scss
// Define a Fibonacci function that takes $n as a parameter
@function fibonacci($n) {
// Initialize the Fibonacci sequence with 0 and 1
  $sequence: 0 1;
// Loop from 1 to $n
  @for $_ from 1 through $n {
	// In Sass, the `nth()` function is used to retrieve an item from a list at a specific position.
	// Calculate the next number in the sequence
    $new: nth($sequence, length($sequence)) + nth($sequence, length($sequence) - 1);
	// Append the new number to the sequence
    $sequence: append($sequence, $new);
  }
// Return the nth Fibonacci number
  @return nth($sequence, length($sequence));
}

.sidebar {
// Set the sidebar float to the left
  float: left;
// Set margin-left to the 4th Fibonacci number multiplied by 1px
  margin-left: fibonacci(4) * 1px;
}
```
## @extend

```scss
.error {
  border: 1px #f00;
  background-color: #fdd;

  &--serious {
    @extend .error;
    border-width: 3px;
  }
}
```
## @at-root

- The `@at-root` rule outputs its contents at the root level, bypassing normal nesting.
- It's commonly used with the parent selector (`&`) and selector functions for more advanced nesting control.

```scss
@use "sass:selector";

@mixin unify-parent($child) {
  @at-root #{selector.unify(&, $child)} {
    @content;
  }
}

.wrapper .field {
  @include unify-parent("input") { }
  @include unify-parent("select") { }
}

// after compiling to css
.wrapper input.field { }
.wrapper select.field { }
```


## Others

`@if`,`@else`,`@each`,`@for`,`@while`,`@media`,`@supports`,`@keyframes`


```scss
$bg-color: blue;
$font-color: dark;

body {
  background-color: if($bg-color == blue, lightblue, white);
  
  @if $font-color == light {
    color: white;
  } @else {
    color: black;
  }
}

$colors: red, green, blue;

@each $color in $colors {
  .box-#{$color} {
    background-color: $color;
  }
}

@for $i from 1 through 3 {
  .item-#{$i} {
    width: 100px * $i;
  }
}

$i: 1;

@while $i <= 3 {
  .circle-#{$i} {
    border-radius: 50% * $i;
    width: 50px * $i;
    height: 50px * $i;
  }
  $i: $i + 1;
}

@media screen and (min-width: 600px) {
  .responsive-box {
    width: 80%;
  }
}

@supports (display: grid) {
  .grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}

@keyframes slide {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100%);
  }
}

.slider {
  animation: slide 2s infinite;
}
```

# Q9: What do built-in modules provide?

TODO
- global
- sass:color
- sass:list
- sass:map
- sass:math
- sass:meta
- sass:selector
- sass:string
# Q10: What APIs does JavaScript provide?

- Core APIs
	- compile(path: string, options?: [Options](https://sass-lang.com/documentation/js-api/interfaces/Options)<"sync">): [CompileResult](https://sass-lang.com/documentation/js-api/interfaces/CompileResult)
	- [Options](https://sass-lang.com/documentation/js-api/interfaces/options/)




