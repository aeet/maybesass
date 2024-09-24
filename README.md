The article is about reading and understanding the foundational source code of bootstrap.
# 1. The basic variable & Color & Theme
- Each UI framework has its own set of variables
- The variables includes predefined values for
	- colors
	- layout
	- spacing
	- dimensions
	- others
- The variable table reflects the overall design standards.
## 1.1 Colors

- First let's talk about grayscale colors.
- Grayscale colors determine the brightness and darkness levels of a webpage.

```scss
$white:    #FAFAFA !default;   
$gray-100: #F0F4F8 !default;   
$gray-200: #D9E3E8 !default;   
$gray-300: #C5C9CC !default;   
$gray-400: #A8B2B6 !default;   
$gray-500: #7D8285 !default;   
$gray-600: #5A5C5E !default;   
$gray-700: #434446 !default;   
$gray-800: #2C2E30 !default;   
$gray-900: #1A1B1C !default;   
$black:    #0A0A0A !default; 
```

- Next, a grayscale color map is defined to facilitate its use in subsequent mixing and functions.

```scss
$grays: (  
  "100": $gray-100,  
  "200": $gray-200,  
  "300": $gray-300,  
  "400": $gray-400,  
  "500": $gray-500,  
  "600": $gray-600,  
  "700": $gray-700,  
  "800": $gray-800,  
  "900": $gray-900  
) !default;
```

- Next comes the color palette, where colors are considered from the perspective of the color wheel, with a different color at every $x$ degrees of the 360° circle.

```scss
$blue:    #A4C8E1 !default;  
$indigo:  #8A9BCA !default;  
$purple:  #BDA0C6 !default;  
$pink:    #E1B7D2 !default;  
$red:     #D3A6A1 !default;  
$orange:  #F1C6A8 !default;  
$yellow:  #E4D6A3 !default;  
$green:   #A8D8B0 !default;  
$teal:    #B0E0E1 !default;  
$cyan:    #B2D6E6 !default;

$colors: (  
  "blue":       $blue,  
  "indigo":     $indigo,  
  "purple":     $purple,  
  "pink":       $pink,  
  "red":        $red,  
  "orange":     $orange,  
  "yellow":     $yellow,  
  "green":      $green,  
  "teal":       $teal,  
  "cyan":       $cyan,  
  "black":      $black,  
  "white":      $white,  
  "gray":       $gray-600,  
  "gray-dark":  $gray-800  
) !default;
```

- Here, some color-mixing mixins/functions are introduced to blend colors efficiently.

```scss
// Mix the given color with a specified proportion of white to lighten the color.
@function tint-color($color, $weight) {  
  @return mix(white, $color, $weight);  
}
// Mix the given color with a specified proportion of white to darken the color.
@function shade-color($color, $weight) {  
  @return mix(black, $color, $weight);  
}
// Shade the color if the weight is positive, else tint it
@function shift-color($color, $weight) {  
  @return if($weight > 0, shade-color($color, $weight), tint-color($color, -$weight));  
}
```

- Next is  color minxing.

```scss
$blue-100: tint-color($blue, 80%) !default;  
$blue-200: tint-color($blue, 60%) !default;  
$blue-300: tint-color($blue, 40%) !default;  
$blue-400: tint-color($blue, 20%) !default;  
$blue-500: $blue !default;  
$blue-600: shade-color($blue, 20%) !default;  
$blue-700: shade-color($blue, 40%) !default;  
$blue-800: shade-color($blue, 60%) !default;  
$blue-900: shade-color($blue, 80%) !default;  
  
$indigo-100: tint-color($indigo, 80%) !default;  
$indigo-200: tint-color($indigo, 60%) !default;  
$indigo-300: tint-color($indigo, 40%) !default;  
$indigo-400: tint-color($indigo, 20%) !default;  
$indigo-500: $indigo !default;  
$indigo-600: shade-color($indigo, 20%) !default;  
$indigo-700: shade-color($indigo, 40%) !default;  
$indigo-800: shade-color($indigo, 60%) !default;  
$indigo-900: shade-color($indigo, 80%) !default;  
  
$purple-100: tint-color($purple, 80%) !default;  
$purple-200: tint-color($purple, 60%) !default;  
$purple-300: tint-color($purple, 40%) !default;  
$purple-400: tint-color($purple, 20%) !default;  
$purple-500: $purple !default;  
$purple-600: shade-color($purple, 20%) !default;  
$purple-700: shade-color($purple, 40%) !default;  
$purple-800: shade-color($purple, 60%) !default;  
$purple-900: shade-color($purple, 80%) !default;  
  
$pink-100: tint-color($pink, 80%) !default;  
$pink-200: tint-color($pink, 60%) !default;  
$pink-300: tint-color($pink, 40%) !default;  
$pink-400: tint-color($pink, 20%) !default;  
$pink-500: $pink !default;  
$pink-600: shade-color($pink, 20%) !default;  
$pink-700: shade-color($pink, 40%) !default;  
$pink-800: shade-color($pink, 60%) !default;  
$pink-900: shade-color($pink, 80%) !default;  
  
$red-100: tint-color($red, 80%) !default;  
$red-200: tint-color($red, 60%) !default;  
$red-300: tint-color($red, 40%) !default;  
$red-400: tint-color($red, 20%) !default;  
$red-500: $red !default;  
$red-600: shade-color($red, 20%) !default;  
$red-700: shade-color($red, 40%) !default;  
$red-800: shade-color($red, 60%) !default;  
$red-900: shade-color($red, 80%) !default;  
  
$orange-100: tint-color($orange, 80%) !default;  
$orange-200: tint-color($orange, 60%) !default;  
$orange-300: tint-color($orange, 40%) !default;  
$orange-400: tint-color($orange, 20%) !default;  
$orange-500: $orange !default;  
$orange-600: shade-color($orange, 20%) !default;  
$orange-700: shade-color($orange, 40%) !default;  
$orange-800: shade-color($orange, 60%) !default;  
$orange-900: shade-color($orange, 80%) !default;  
  
$yellow-100: tint-color($yellow, 80%) !default;  
$yellow-200: tint-color($yellow, 60%) !default;  
$yellow-300: tint-color($yellow, 40%) !default;  
$yellow-400: tint-color($yellow, 20%) !default;  
$yellow-500: $yellow !default;  
$yellow-600: shade-color($yellow, 20%) !default;  
$yellow-700: shade-color($yellow, 40%) !default;  
$yellow-800: shade-color($yellow, 60%) !default;  
$yellow-900: shade-color($yellow, 80%) !default;  
  
$green-100: tint-color($green, 80%) !default;  
$green-200: tint-color($green, 60%) !default;  
$green-300: tint-color($green, 40%) !default;  
$green-400: tint-color($green, 20%) !default;  
$green-500: $green !default;  
$green-600: shade-color($green, 20%) !default;  
$green-700: shade-color($green, 40%) !default;  
$green-800: shade-color($green, 60%) !default;  
$green-900: shade-color($green, 80%) !default;  
  
$teal-100: tint-color($teal, 80%) !default;  
$teal-200: tint-color($teal, 60%) !default;  
$teal-300: tint-color($teal, 40%) !default;  
$teal-400: tint-color($teal, 20%) !default;  
$teal-500: $teal !default;  
$teal-600: shade-color($teal, 20%) !default;  
$teal-700: shade-color($teal, 40%) !default;  
$teal-800: shade-color($teal, 60%) !default;  
$teal-900: shade-color($teal, 80%) !default;  
  
$cyan-100: tint-color($cyan, 80%) !default;  
$cyan-200: tint-color($cyan, 60%) !default;  
$cyan-300: tint-color($cyan, 40%) !default;  
$cyan-400: tint-color($cyan, 20%) !default;  
$cyan-500: $cyan !default;  
$cyan-600: shade-color($cyan, 20%) !default;  
$cyan-700: shade-color($cyan, 40%) !default;  
$cyan-800: shade-color($cyan, 60%) !default;  
$cyan-900: shade-color($cyan, 80%) !default;  
  
$blues: (  
  "blue-100": $blue-100,  
  "blue-200": $blue-200,  
  "blue-300": $blue-300,  
  "blue-400": $blue-400,  
  "blue-500": $blue-500,  
  "blue-600": $blue-600,  
  "blue-700": $blue-700,  
  "blue-800": $blue-800,  
  "blue-900": $blue-900  
) !default;  
  
$indigos: (  
  "indigo-100": $indigo-100,  
  "indigo-200": $indigo-200,  
  "indigo-300": $indigo-300,  
  "indigo-400": $indigo-400,  
  "indigo-500": $indigo-500,  
  "indigo-600": $indigo-600,  
  "indigo-700": $indigo-700,  
  "indigo-800": $indigo-800,  
  "indigo-900": $indigo-900  
) !default;  
  
$purples: (  
  "purple-100": $purple-100,  
  "purple-200": $purple-200,  
  "purple-300": $purple-300,  
  "purple-400": $purple-400,  
  "purple-500": $purple-500,  
  "purple-600": $purple-600,  
  "purple-700": $purple-700,  
  "purple-800": $purple-800,  
  "purple-900": $purple-900  
) !default;  
  
$pinks: (  
  "pink-100": $pink-100,  
  "pink-200": $pink-200,  
  "pink-300": $pink-300,  
  "pink-400": $pink-400,  
  "pink-500": $pink-500,  
  "pink-600": $pink-600,  
  "pink-700": $pink-700,  
  "pink-800": $pink-800,  
  "pink-900": $pink-900  
) !default;  
  
$reds: (  
  "red-100": $red-100,  
  "red-200": $red-200,  
  "red-300": $red-300,  
  "red-400": $red-400,  
  "red-500": $red-500,  
  "red-600": $red-600,  
  "red-700": $red-700,  
  "red-800": $red-800,  
  "red-900": $red-900  
) !default;  
  
$oranges: (  
  "orange-100": $orange-100,  
  "orange-200": $orange-200,  
  "orange-300": $orange-300,  
  "orange-400": $orange-400,  
  "orange-500": $orange-500,  
  "orange-600": $orange-600,  
  "orange-700": $orange-700,  
  "orange-800": $orange-800,  
  "orange-900": $orange-900  
) !default;  
  
$yellows: (  
  "yellow-100": $yellow-100,  
  "yellow-200": $yellow-200,  
  "yellow-300": $yellow-300,  
  "yellow-400": $yellow-400,  
  "yellow-500": $yellow-500,  
  "yellow-600": $yellow-600,  
  "yellow-700": $yellow-700,  
  "yellow-800": $yellow-800,  
  "yellow-900": $yellow-900  
) !default;  
  
$greens: (  
  "green-100": $green-100,  
  "green-200": $green-200,  
  "green-300": $green-300,  
  "green-400": $green-400,  
  "green-500": $green-500,  
  "green-600": $green-600,  
  "green-700": $green-700,  
  "green-800": $green-800,  
  "green-900": $green-900  
) !default;  
  
$teals: (  
  "teal-100": $teal-100,  
  "teal-200": $teal-200,  
  "teal-300": $teal-300,  
  "teal-400": $teal-400,  
  "teal-500": $teal-500,  
  "teal-600": $teal-600,  
  "teal-700": $teal-700,  
  "teal-800": $teal-800,  
  "teal-900": $teal-900  
) !default;  
  
$cyans: (  
  "cyan-100": $cyan-100,  
  "cyan-200": $cyan-200,  
  "cyan-300": $cyan-300,  
  "cyan-400": $cyan-400,  
  "cyan-500": $cyan-500,  
  "cyan-600": $cyan-600,  
  "cyan-700": $cyan-700,  
  "cyan-800": $cyan-800,  
  "cyan-900": $cyan-900  
) !default;
```

- Then define the website's theme color.

```scss
$primary:       $blue !default;  
$secondary:     $gray-600 !default;  
$success:       $green !default;  
$info:          $cyan !default;  
$warning:       $yellow !default;  
$danger:        $red !default;  
$light:         $gray-100 !default;  
$dark:          $gray-900 !default;

$theme-colors: (  
  "primary":    $primary,  
  "secondary":  $secondary,  
  "success":    $success,  
  "info":       $info,  
  "warning":    $warning,  
  "danger":     $danger,  
  "light":      $light,  
  "dark":       $dark  
) !default;
```

- Define the text colors

```scss
$primary-text-emphasis:   shade-color($primary, 60%) !default;  
$secondary-text-emphasis: shade-color($secondary, 60%) !default;  
$success-text-emphasis:   shade-color($success, 60%) !default;  
$info-text-emphasis:      shade-color($info, 60%) !default;  
$warning-text-emphasis:   shade-color($warning, 60%) !default;  
$danger-text-emphasis:    shade-color($danger, 60%) !default;  
$light-text-emphasis:     $gray-700 !default;  
$dark-text-emphasis:      $gray-700 !default;
```

- Background colors

```scss
$primary-bg-subtle:       tint-color($primary, 80%) !default;  
$secondary-bg-subtle:     tint-color($secondary, 80%) !default;  
$success-bg-subtle:       tint-color($success, 80%) !default;  
$info-bg-subtle:          tint-color($info, 80%) !default;  
$warning-bg-subtle:       tint-color($warning, 80%) !default;  
$danger-bg-subtle:        tint-color($danger, 80%) !default;  
$light-bg-subtle:         mix($gray-100, $white) !default;  
$dark-bg-subtle:          $gray-400 !default;
```

- Border colors

```scss
$primary-border-subtle:   tint-color($primary, 60%) !default;  
$secondary-border-subtle: tint-color($secondary, 60%) !default;  
$success-border-subtle:   tint-color($success, 60%) !default;  
$info-border-subtle:      tint-color($info, 60%) !default;  
$warning-border-subtle:   tint-color($warning, 60%) !default;  
$danger-border-subtle:    tint-color($danger, 60%) !default;  
$light-border-subtle:     $gray-200 !default;  
$dark-border-subtle:      $gray-500 !default;
```

## 1.2 Options

- These options are used to enable or disable certain features(at compile time) and change the execution branches of functions or mixins.

```scss
$enable-caret:                true !default;  
$enable-rounded:              true !default;  
$enable-shadows:              false !default;  
$enable-gradients:            false !default;  
$enable-transitions:          true !default;  
$enable-reduced-motion:       true !default;  
$enable-smooth-scroll:        true !default;  
$enable-grid-classes:         true !default;  
$enable-container-classes:    true !default;  
$enable-cssgrid:              false !default;  
$enable-button-pointers:      true !default;  
$enable-rfs:                  true !default;  
$enable-validation-icons:     true !default;  
$enable-negative-margins:     false !default;  
$enable-deprecation-messages: true !default;  
$enable-important-utilities:  true !default;
$enable-dark-mode:            true !default;
```

## 1.3 Theme

- Let’s focus on `dark-mode` and `$color-mode-type` to understand how to control the theme.
- `$color-mode-type` has two values: one is `data` and the other is `media-query`.

```scss
$enable-dark-mode:            true !default;
$color-mode-type:             data !default; // `data` or `media-query`
```

- `color-mode` is a mixin that accepts two parameters: one is `mode` and the other is `false`.
- Specify different primary styles through various options.
- Then use external content to fill in the `@content`.

```scss
@mixin color-mode($mode: light, $root: false) {  
  @if $color-mode-type == "media-query" {  
    @if $root == true {  
      @media (prefers-color-scheme: $mode) {  
        :root {  
          @content;  
        }  
      }  
    } @else {  
      @media (prefers-color-scheme: $mode) {  
        @content;  
      }  
    }  
  } @else {  
    [data-bs-theme="#{$mode}"] {  
      @content;  
    }  
  }  
}  
```

- When the value of `data-bs-theme` is defined as `light` under `:root`, each variable is bound to its corresponding color.

``` scss
:root,  
[data-bs-theme="light"] {  
  @each $color, $value in $colors {  
    --#{$prefix}#{$color}: #{$value};  
  }  
  
  @each $color, $value in $grays {  
    --#{$prefix}gray-#{$color}: #{$value};  
  }  
  
  @each $color, $value in $theme-colors {  
    --#{$prefix}#{$color}: #{$value};  
  }  
  
  @each $color, $value in $theme-colors-rgb {  
    --#{$prefix}#{$color}-rgb: #{$value};  
  }  
  
  @each $color, $value in $theme-colors-text {  
    --#{$prefix}#{$color}-text-emphasis: #{$value};  
  }  
  
  @each $color, $value in $theme-colors-bg-subtle {  
    --#{$prefix}#{$color}-bg-subtle: #{$value};  
  }  
  
  @each $color, $value in $theme-colors-border-subtle {  
    --#{$prefix}#{$color}-border-subtle: #{$value};  
  }  
  
  --#{$prefix}white-rgb: #{to-rgb($white)};  
  --#{$prefix}black-rgb: #{to-rgb($black)};  
  
  --#{$prefix}font-monospace: #{inspect($font-family-monospace)};  
  --#{$prefix}gradient: #{$gradient};  
  
    --#{$prefix}root-font-size: #{$font-size-root};  
  }  
  --#{$prefix}body-font-family: #{inspect($font-family-base)};  
  @include rfs($font-size-base, --#{$prefix}body-font-size);  
  --#{$prefix}body-font-weight: #{$font-weight-base};  
  --#{$prefix}body-line-height: #{$line-height-base};  
  @if $body-text-align != null {  
    --#{$prefix}body-text-align: #{$body-text-align};  
  }  
  
  --#{$prefix}body-color: #{$body-color};  
  --#{$prefix}body-color-rgb: #{to-rgb($body-color)};  
  --#{$prefix}body-bg: #{$body-bg};  
  --#{$prefix}body-bg-rgb: #{to-rgb($body-bg)};  
  
  --#{$prefix}emphasis-color: #{$body-emphasis-color};  
  --#{$prefix}emphasis-color-rgb: #{to-rgb($body-emphasis-color)};  
  
  --#{$prefix}secondary-color: #{$body-secondary-color};  
  --#{$prefix}secondary-color-rgb: #{to-rgb($body-secondary-color)};  
  --#{$prefix}secondary-bg: #{$body-secondary-bg};  
  --#{$prefix}secondary-bg-rgb: #{to-rgb($body-secondary-bg)};  
  
  --#{$prefix}tertiary-color: #{$body-tertiary-color};  
  --#{$prefix}tertiary-color-rgb: #{to-rgb($body-tertiary-color)};  
  --#{$prefix}tertiary-bg: #{$body-tertiary-bg};  
  --#{$prefix}tertiary-bg-rgb: #{to-rgb($body-tertiary-bg)};  
  // scss-docs-end root-body-variables  
  
  --#{$prefix}heading-color: #{$headings-color};  
  
  --#{$prefix}link-color: #{$link-color};  
  --#{$prefix}link-color-rgb: #{to-rgb($link-color)};  
  --#{$prefix}link-decoration: #{$link-decoration};  
  
  --#{$prefix}link-hover-color: #{$link-hover-color};  
  --#{$prefix}link-hover-color-rgb: #{to-rgb($link-hover-color)};  
  
  @if $link-hover-decoration != null {  
    --#{$prefix}link-hover-decoration: #{$link-hover-decoration};  
  }  
  
  --#{$prefix}code-color: #{$code-color};  
  --#{$prefix}highlight-color: #{$mark-color};  
  --#{$prefix}highlight-bg: #{$mark-bg};  
  
  // scss-docs-start root-border-var  
  --#{$prefix}border-width: #{$border-width};  
  --#{$prefix}border-style: #{$border-style};  
  --#{$prefix}border-color: #{$border-color};  
  --#{$prefix}border-color-translucent: #{$border-color-translucent};  
  
  --#{$prefix}border-radius: #{$border-radius};  
  --#{$prefix}border-radius-sm: #{$border-radius-sm};  
  --#{$prefix}border-radius-lg: #{$border-radius-lg};  
  --#{$prefix}border-radius-xl: #{$border-radius-xl};  
  --#{$prefix}border-radius-xxl: #{$border-radius-xxl};  
  --#{$prefix}border-radius-2xl: var(--#{$prefix}border-radius-xxl);   
  --#{$prefix}border-radius-pill: #{$border-radius-pill};  
  
  --#{$prefix}box-shadow: #{$box-shadow};  
  --#{$prefix}box-shadow-sm: #{$box-shadow-sm};  
  --#{$prefix}box-shadow-lg: #{$box-shadow-lg};  
  --#{$prefix}box-shadow-inset: #{$box-shadow-inset};  
  
  --#{$prefix}focus-ring-opacity: #{$focus-ring-opacity};  
  --#{$prefix}focus-ring-color: #{$focus-ring-color};  
  --#{$prefix}form-valid-border-color: #{$form-valid-border-color};  
  --#{$prefix}form-invalid-color: #{$form-invalid-color};  
  --#{$prefix}form-invalid-border-color: #{$form-invalid-border-color};  
}
```

- call color-mode mixin

```scss
@if $enable-dark-mode {  
  @include color-mode(dark, true) {  
	color-scheme: dark;  

	--#{$prefix}body-color: #{$body-color-dark};  
	--#{$prefix}body-color-rgb: #{to-rgb($body-color-dark)};  
	--#{$prefix}body-bg: #{$body-bg-dark};  
	--#{$prefix}body-bg-rgb: #{to-rgb($body-bg-dark)};
	......
  }
}
```

- after compilation.

```scss
:root,  
[data-bs-theme=light] {  
  --bs-blue: #A4C8E1;  
  --bs-indigo: #8A9BCA;  
  --bs-purple: #BDA0C6;  
  --bs-pink: #E1B7D2;  
  --bs-red: #D3A6A1;  
  --bs-orange: #F1C6A8;  
  --bs-yellow: #E4D6A3;  
  --bs-green: #A8D8B0;  
  --bs-teal: #B0E0E1;  
  --bs-cyan: #B2D6E6;  
  --bs-black: #0A0A0A;  
  --bs-white: #FAFAFA;  
  --bs-gray: #5A5C5E;  
  --bs-gray-dark: #2C2E30;  
  --bs-gray-100: #F0F4F8;  
  --bs-gray-200: #D9E3E8;  
  --bs-gray-300: #C5C9CC;  
  --bs-gray-400: #A8B2B6;  
  --bs-gray-500: #7D8285;  
  --bs-gray-600: #5A5C5E;  
  --bs-gray-700: #434446;  
  --bs-gray-800: #2C2E30;  
  --bs-gray-900: #1A1B1C;  
  --bs-primary: #A4C8E1;  
  --bs-secondary: #5A5C5E;  
  --bs-success: #A8D8B0;  
  --bs-info: #B2D6E6;  
  --bs-warning: #E4D6A3;  
  --bs-danger: #D3A6A1;  
  --bs-light: #F0F4F8;  
  --bs-dark: #1A1B1C;  
  --bs-primary-rgb: 164, 200, 225;  
  --bs-secondary-rgb: 90, 92, 94;  
  --bs-success-rgb: 168, 216, 176;  
  --bs-info-rgb: 178, 214, 230;  
  --bs-warning-rgb: 228, 214, 163;  
  --bs-danger-rgb: 211, 166, 161;  
  --bs-light-rgb: 240, 244, 248;  
  --bs-dark-rgb: 26, 27, 28;  
  --bs-primary-text-emphasis: rgb(65.6, 80, 90);  
  --bs-secondary-text-emphasis: rgb(36, 36.8, 37.6);  
  --bs-success-text-emphasis: rgb(67.2, 86.4, 70.4);  
  --bs-info-text-emphasis: rgb(71.2, 85.6, 92);  
  --bs-warning-text-emphasis: rgb(91.2, 85.6, 65.2);  
  --bs-danger-text-emphasis: rgb(84.4, 66.4, 64.4);  
  --bs-light-text-emphasis: #434446;  
  --bs-dark-text-emphasis: #434446;  
  --bs-primary-bg-subtle: rgb(236.8, 244, 249);  
  --bs-secondary-bg-subtle: rgb(222, 222.4, 222.8);  
  --bs-success-bg-subtle: rgb(237.6, 247.2, 239.2);  
  --bs-info-bg-subtle: rgb(239.6, 246.8, 250);  
  --bs-warning-bg-subtle: rgb(249.6, 246.8, 236.6);  
  --bs-danger-bg-subtle: rgb(246.2, 237.2, 236.2);  
  --bs-light-bg-subtle: #f5f7f9;  
  --bs-dark-bg-subtle: #A8B2B6;  
  --bs-primary-border-subtle: rgb(218.6, 233, 243);  
  --bs-secondary-border-subtle: rgb(189, 189.8, 190.6);  
  --bs-success-border-subtle: rgb(220.2, 239.4, 223.4);  
  --bs-info-border-subtle: rgb(224.2, 238.6, 245);  
  --bs-warning-border-subtle: rgb(244.2, 238.6, 218.2);  
  --bs-danger-border-subtle: rgb(237.4, 219.4, 217.4);  
  --bs-light-border-subtle: #D9E3E8;  
  --bs-dark-border-subtle: #7D8285;  
  --bs-white-rgb: 250, 250, 250;  
  --bs-black-rgb: 10, 10, 10;  
  --bs-font-sans-serif: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", "Noto Sans", "Liberation Sans", Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";  
  --bs-font-monospace: SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;  
  --bs-gradient: linear-gradient(180deg, rgba(250, 250, 250, 0.15), rgba(250, 250, 250, 0));  
  --bs-body-font-family: var(--bs-font-sans-serif);  
  --bs-body-font-size: 1rem;  
  --bs-body-font-weight: 400;  
  --bs-body-line-height: 1.5;  
  --bs-body-color: #1A1B1C;  
  --bs-body-color-rgb: 26, 27, 28;  
  --bs-body-bg: #FAFAFA;  
  --bs-body-bg-rgb: 250, 250, 250;  
  --bs-emphasis-color: #0A0A0A;  
  --bs-emphasis-color-rgb: 10, 10, 10;  
  --bs-secondary-color: rgba(26, 27, 28, 0.75);  
  --bs-secondary-color-rgb: 26, 27, 28;  
  --bs-secondary-bg: #D9E3E8;  
  --bs-secondary-bg-rgb: 217, 227, 232;  
  --bs-tertiary-color: rgba(26, 27, 28, 0.5);  
  --bs-tertiary-color-rgb: 26, 27, 28;  
  --bs-tertiary-bg: #F0F4F8;  
  --bs-tertiary-bg-rgb: 240, 244, 248;  
  --bs-heading-color: inherit;  
  --bs-link-color: #A4C8E1;  
  --bs-link-color-rgb: 164, 200, 225;  
  --bs-link-decoration: underline;  
  --bs-link-hover-color: rgb(131.2, 160, 180);  
  --bs-link-hover-color-rgb: 131, 160, 180;  
  --bs-code-color: #E1B7D2;  
  --bs-highlight-color: #1A1B1C;  
  --bs-highlight-bg: rgb(249.6, 246.8, 236.6);  
  --bs-border-width: 1px;  
  --bs-border-style: solid;  
  --bs-border-color: #C5C9CC;  
  --bs-border-color-translucent: rgba(10, 10, 10, 0.175);  
  --bs-border-radius: 0.375rem;  
  --bs-border-radius-sm: 0.25rem;  
  --bs-border-radius-lg: 0.5rem;  
  --bs-border-radius-xl: 1rem;  
  --bs-border-radius-xxl: 2rem;  
  --bs-border-radius-2xl: var(--bs-border-radius-xxl);  
  --bs-border-radius-pill: 50rem;  
  --bs-box-shadow: 0 0.5rem 1rem rgba(10, 10, 10, 0.15);  
  --bs-box-shadow-sm: 0 0.125rem 0.25rem rgba(10, 10, 10, 0.075);  
  --bs-box-shadow-lg: 0 1rem 3rem rgba(10, 10, 10, 0.175);  
  --bs-box-shadow-inset: inset 0 1px 2px rgba(10, 10, 10, 0.075);  
  --bs-focus-ring-width: 0.25rem;  
  --bs-focus-ring-opacity: 0.25;  
  --bs-focus-ring-color: rgba(164, 200, 225, 0.25);  
  --bs-form-valid-color: #A8D8B0;  
  --bs-form-valid-border-color: #A8D8B0;  
  --bs-form-invalid-color: #D3A6A1;  
  --bs-form-invalid-border-color: #D3A6A1;  
}  
  
[data-bs-theme=dark] {  
  color-scheme: dark;  
  --bs-body-color: #C5C9CC;  
  --bs-body-color-rgb: 197, 201, 204;  
  --bs-body-bg: #1A1B1C;  
  --bs-body-bg-rgb: 26, 27, 28;  
  --bs-emphasis-color: #FAFAFA;  
  --bs-emphasis-color-rgb: 250, 250, 250;  
  --bs-secondary-color: rgba(197, 201, 204, 0.75);  
  --bs-secondary-color-rgb: 197, 201, 204;  
  --bs-secondary-bg: #2C2E30;  
  --bs-secondary-bg-rgb: 44, 46, 48;  
  --bs-tertiary-color: rgba(197, 201, 204, 0.5);  
  --bs-tertiary-color-rgb: 197, 201, 204;  
  --bs-tertiary-bg: rgb(35, 36.5, 38);  
  --bs-tertiary-bg-rgb: 35, 37, 38;  
  --bs-primary-text-emphasis: rgb(200.4, 222, 237);  
  --bs-secondary-text-emphasis: rgb(156, 157.2, 158.4);  
  --bs-success-text-emphasis: rgb(202.8, 231.6, 207.6);  
  --bs-info-text-emphasis: rgb(208.8, 230.4, 240);  
  --bs-warning-text-emphasis: rgb(238.8, 230.4, 199.8);  
  --bs-danger-text-emphasis: rgb(228.6, 201.6, 198.6);  
  --bs-light-text-emphasis: #F0F4F8;  
  --bs-dark-text-emphasis: #C5C9CC;  
  --bs-primary-bg-subtle: rgb(32.8, 40, 45);  
  --bs-secondary-bg-subtle: rgb(18, 18.4, 18.8);  
  --bs-success-bg-subtle: rgb(33.6, 43.2, 35.2);  
  --bs-info-bg-subtle: rgb(35.6, 42.8, 46);  
  --bs-warning-bg-subtle: rgb(45.6, 42.8, 32.6);  
  --bs-danger-bg-subtle: rgb(42.2, 33.2, 32.2);  
  --bs-light-bg-subtle: #2C2E30;  
  --bs-dark-bg-subtle: #1b1c1d;  
  --bs-primary-border-subtle: rgb(98.4, 120, 135);  
  --bs-secondary-border-subtle: rgb(54, 55.2, 56.4);  
  --bs-success-border-subtle: rgb(100.8, 129.6, 105.6);  
  --bs-info-border-subtle: rgb(106.8, 128.4, 138);  
  --bs-warning-border-subtle: rgb(136.8, 128.4, 97.8);  
  --bs-danger-border-subtle: rgb(126.6, 99.6, 96.6);  
  --bs-light-border-subtle: #434446;  
  --bs-dark-border-subtle: #2C2E30;  
  --bs-heading-color: inherit;  
  --bs-link-color: rgb(200.4, 222, 237);  
  --bs-link-hover-color: rgb(211.32, 228.6, 240.6);  
  --bs-link-color-rgb: 200, 222, 237;  
  --bs-link-hover-color-rgb: 211, 229, 241;  
  --bs-code-color: rgb(237, 211.8, 228);  
  --bs-highlight-color: #C5C9CC;  
  --bs-highlight-bg: rgb(91.2, 85.6, 65.2);  
  --bs-border-color: #434446;  
  --bs-border-color-translucent: rgba(250, 250, 250, 0.15);  
  --bs-form-valid-color: rgb(202.8, 231.6, 207.6);  
  --bs-form-valid-border-color: rgb(202.8, 231.6, 207.6);  
  --bs-form-invalid-color: rgb(228.6, 201.6, 198.6);  
  --bs-form-invalid-border-color: rgb(228.6, 201.6, 198.6);
}
```

- When we want to switch themes, we just need to add the `data-bs-theme` attribute to the body.

# 2. Layout

Bootstrap providers grid and container layout systems.


```scss
// `container-max-widths` provides a width map for different device screen sizes.
$container-max-widths: (  
  sm: 540px,  
  md: 720px,  
  lg: 960px,  
  xl: 1140px,  
  xxl: 1320px  
) !default;

$grid-breakpoints: (  
  xs: 0,  
  sm: 576px,  
  md: 768px,  
  lg: 992px,  
  xl: 1200px,  
  xxl: 1400px  
) !default;

$grid-gutter-width:           1.5rem !default;

$container-padding-x: $grid-gutter-width !default;

// `make-container` can accept a gutter value or default to 1.5rem.
@mixin make-container($gutter: $container-padding-x) {  
  --#{$prefix}gutter-x: #{$gutter};  
  --#{$prefix}gutter-y: 0;  
  width: 100%;  
  padding-right: calc(var(--#{$prefix}gutter-x) * .5); // stylelint-disable-line function-disallowed-list  
  padding-left: calc(var(--#{$prefix}gutter-x) * .5); // stylelint-disable-line function-disallowed-list  
  margin-right: auto;  
  margin-left: auto;  
}

// extract the corresponding values from a predefined breakpoint map.
@function breakpoint-min($name, $breakpoints: $grid-breakpoints) {  
  $min: map-get($breakpoints, $name);  
  @return if($min != 0, $min, null);  
}

// extract the widths to create media queries for each width.
@mixin media-breakpoint-up($name, $breakpoints: $grid-breakpoints) {  
  $min: breakpoint-min($name, $breakpoints);  
  @if $min {  
    @media (min-width: $min) {  
      @content;  
    }  
  } @else {  
    @content;  
  }  
}

@function breakpoint-infix($name, $breakpoints: $grid-breakpoints) {  
  @return if(breakpoint-min($name, $breakpoints) == null, "", "-#{$name}");  
}

```

- Then, the actual style writing for the container begins.

```scss
// `$enable-container-classes` is a compilation option.
@if $enable-container-classes {  
// Single container class with breakpoint max-widths  
  .container,  
// 100% wide container at all breakpoints  
  .container-fluid {  
	// Calling `make-container` without passing a value will use the default settings.
    @include make-container();  
  }  
  
 // Responsive containers that are 100% wide until a breakpoint  
 // Iterate through the keys and values of the map. 
  @each $breakpoint, $container-max-width in $container-max-widths {  
     // .container-xl|md|xxl|xs ....
    .container-#{$breakpoint} {  
	  // make-container() 
      @extend .container-fluid;  
    }  

	// @media (min-width: 576px|768px|992px...) {max-width: 540px|720px....}
	//  the width ranges are defined through the grid and container.
    @include media-breakpoint-up($breakpoint, $grid-breakpoints) {  
	// `%responsive` is a placeholder selector. Selectors starting with `%` cannot be applied directly but can be inherited by other selectors using `@extend`.
	//  container-xl|md|xxl|xs...{max-width} 
      %responsive-container-#{$breakpoint} {  
        max-width: $container-max-width;  
      }  
  
      // Extend each breakpoint which is smaller or equal to the current breakpoint  
      $extend-breakpoint: true;  
	  //  Iterate through the map.
      @each $name, $width in $grid-breakpoints {  
        @if ($extend-breakpoint) {  
          // like .container-md, .container-sm, .container{}
          .container#{breakpoint-infix($name, $grid-breakpoints)} {  
            @extend %responsive-container-#{$breakpoint};  
          }  
  
          // Once the current breakpoint is reached, stop extending  
          @if ($breakpoint == $name) {  
            $extend-breakpoint: false;  
          }  
        }  
      }  
    }  
  }  
}
```

- After compile

```scss
.container,  
.container-fluid,  
.container-xxl,  
.container-xl,  
.container-lg,  
.container-md,  
.container-sm {  
  --bs-gutter-x: 1.5rem;  
  --bs-gutter-y: 0;  
  width: 100%;  
  padding-right: calc(var(--bs-gutter-x) * 0.5);  
  padding-left: calc(var(--bs-gutter-x) * 0.5);  
  margin-right: auto;  
  margin-left: auto;  
}

@media (min-width: 576px) {  
  .container-sm, .container {  
    max-width: 540px;  
  }  
}  
@media (min-width: 768px) {  
  .container-md, .container-sm, .container {  
    max-width: 720px;  
  }  
}  
@media (min-width: 992px) {  
  .container-lg, .container-md, .container-sm, .container {  
    max-width: 960px;  
  }  
}  
@media (min-width: 1200px) {  
  .container-xl, .container-lg, .container-md, .container-sm, .container {  
    max-width: 1140px;  
  }  
}  
@media (min-width: 1400px) {  
  .container-xxl, .container-xl, .container-lg, .container-md, .container-sm, .container {  
    max-width: 1320px;  
  }  
}
```

- The container provides a responsive container.
- The grid provides rows and columns.

```scss
// :root {  
//   --bs-breakpoint-xs: 0;  
//   --bs-breakpoint-sm: 576px;  
//   --bs-breakpoint-md: 768px;  
//   --bs-breakpoint-lg: 992px;  
//   --bs-breakpoint-xl: 1200px;  
//   --bs-breakpoint-xxl: 1400px;  
// }
:root {  
  @each $name, $value in $grid-breakpoints {  
    --#{$prefix}breakpoint-#{$name}: #{$value};  
  }  
}  
  
@if $enable-grid-classes {  
  .row {  
    @include make-row();  
    > * {  
      @include make-col-ready();  
    }  
  }  
}  

@mixin make-row($gutter: $grid-gutter-width) {  
  --#{$prefix}gutter-x: #{$gutter};  
  --#{$prefix}gutter-y: 0;  
  display: flex;  
  flex-wrap: wrap;  
  margin-top: calc(-1 * var(--#{$prefix}gutter-y));  
  margin-right: calc(-.5 * var(--#{$prefix}gutter-x));  
  margin-left: calc(-.5 * var(--#{$prefix}gutter-x)); /
}

@mixin make-col-ready() {  
  box-sizing: if(variable-exists(include-column-box-sizing) and $include-column-box-sizing, border-box, null);  
  width: 100%;  
  max-width: 100%;   
  padding-right: calc(var(--#{$prefix}gutter-x) * .5);   
  padding-left: calc(var(--#{$prefix}gutter-x) * .5);   
  margin-top: var(--#{$prefix}gutter-y);  
}
  
	@if $enable-grid-classes {  
  @include make-grid-columns();  
}
```

- That's the overview of the row. 
- After compilation...
```scss
:root {  
  --bs-breakpoint-xs: 0;  
  --bs-breakpoint-sm: 576px;  
  --bs-breakpoint-md: 768px;  
  --bs-breakpoint-lg: 992px;  
  --bs-breakpoint-xl: 1200px;  
  --bs-breakpoint-xxl: 1400px;  
}  
  
.row {  
  --bs-gutter-x: 1.5rem;  
  --bs-gutter-y: 0;  
  display: flex;  
  flex-wrap: wrap;  
  margin-top: calc(-1 * var(--bs-gutter-y));  
  margin-right: calc(-0.5 * var(--bs-gutter-x));  
  margin-left: calc(-0.5 * var(--bs-gutter-x));  
}  

.row > * {  
  flex-shrink: 0;  
  width: 100%;  
  max-width: 100%;  
  padding-right: calc(var(--bs-gutter-x) * 0.5);  
  padding-left: calc(var(--bs-gutter-x) * 0.5);  
  margin-top: var(--bs-gutter-y);  
}
```

- We just covered rows; now let's see how the styles for columns are generated.


```scss
@mixin make-grid-columns($columns: $grid-columns, $gutter: $grid-gutter-width, $breakpoints: $grid-breakpoints) {
  // Iterate through each breakpoint like xl, md, xxl, etc.
  @each $breakpoint in map-keys($breakpoints) {
    // Get the suffix for the current breakpoint, e.g., -md or -xl
    $infix: breakpoint-infix($breakpoint, $breakpoints);  

    // Create a media query for each breakpoint, e.g., @media (min-width: 768px) { ... }
    @include media-breakpoint-up($breakpoint, $breakpoints) {
      // Define the basic styles for columns, e.g., .col-md { flex: 1 0 0%; }
      .col#{$infix} {  
        flex: 1 0 0%;  // For example: .col-md { flex: 1 0 0%; }
      }  

      // Define styles for automatic columns, e.g., .row-cols-md-auto > * { ... }
      .row-cols#{$infix}-auto > * {  
        @include make-col-auto();  // For example: .row-cols-md-auto > * { width: auto; }
      }  

      // If there are row columns, loop to generate styles
      @if $grid-row-columns > 0 {  
        @for $i from 1 through $grid-row-columns {  
          .row-cols#{$infix}-#{$i} {  
            @include row-cols($i);  // For example: .row-cols-md-2 { display: flex; }
          }  
        }  
      }  

      // Define styles for automatic columns, e.g., .col-md-auto { width: auto; }
      .col#{$infix}-auto {  
        @include make-col-auto();  // For example: .col-md-auto { width: auto; }
      }  

      // If the column count is greater than 0, generate column styles
      @if $columns > 0 {  
        @for $i from 1 through $columns {  
          .col#{$infix}-#{$i} {  
            @include make-col($i, $columns);  // For example: .col-lg-4 { flex: 0 0 33.33%; }
          }  
        }  

        // Generate offset styles
        @for $i from 0 through ($columns - 1) {  
          @if not ($infix == "" and $i == 0) {   
            .offset#{$infix}-#{$i} {  
              @include make-col-offset($i, $columns);  // For example: .offset-sm-2 { margin-left: 16.67%; }
            }  
          }  
        }  
      }  

      // Define styles for horizontal spacing, e.g., .g-md-3 { --bs-gutter-x: 1rem; }
      .g#{$infix}-#{$key},  
      .gx#{$infix}-#{$key} {  
        --#{$prefix}gutter-x: #{$value};  // For example: --bs-gutter-x: 1rem;
      }  

      // Define styles for vertical spacing, e.g., .g-md-3 { --bs-gutter-y: 1rem; }
      .g#{$infix}-#{$key},  
      .gy#{$infix}-#{$key} {  
        --#{$prefix}gutter-y: #{$value};  // For example: --bs-gutter-y: 1rem;
      }  
    }  
  }  
}
```

- After compilation.


```scss
.col {  
  flex: 1 0 0%;  
}  
  
.row-cols-auto > * {  
  flex: 0 0 auto;  
  width: auto;  
}  
  
.row-cols-1 > * {  
  flex: 0 0 auto;  
  width: 100%;  
}  
  
.row-cols-2 > * {  
  flex: 0 0 auto;  
  width: 50%;  
}  
  
.row-cols-3 > * {  
  flex: 0 0 auto;  
  width: 33.33333333%;  
}  
  
.row-cols-4 > * {  
  flex: 0 0 auto;  
  width: 25%;  
}  
  
.row-cols-5 > * {  
  flex: 0 0 auto;  
  width: 20%;  
}  
  
.row-cols-6 > * {  
  flex: 0 0 auto;  
  width: 16.66666667%;  
}  
  
.col-auto {  
  flex: 0 0 auto;  
  width: auto;  
}  
  
.col-1 {  
  flex: 0 0 auto;  
  width: 8.33333333%;  
}  
  
.col-2 {  
  flex: 0 0 auto;  
  width: 16.66666667%;  
}  
  
.col-3 {  
  flex: 0 0 auto;  
  width: 25%;  
}  
  
.col-4 {  
  flex: 0 0 auto;  
  width: 33.33333333%;  
}  
  
.col-5 {  
  flex: 0 0 auto;  
  width: 41.66666667%;  
}  
  
.col-6 {  
  flex: 0 0 auto;  
  width: 50%;  
}  
  
.col-7 {  
  flex: 0 0 auto;  
  width: 58.33333333%;  
}  
  
.col-8 {  
  flex: 0 0 auto;  
  width: 66.66666667%;  
}  
  
.col-9 {  
  flex: 0 0 auto;  
  width: 75%;  
}  
  
.col-10 {  
  flex: 0 0 auto;  
  width: 83.33333333%;  
}  
  
.col-11 {  
  flex: 0 0 auto;  
  width: 91.66666667%;  
}  
  
.col-12 {  
  flex: 0 0 auto;  
  width: 100%;  
}  
  
.offset-1 {  
  margin-left: 8.33333333%;  
}  
  
.offset-2 {  
  margin-left: 16.66666667%;  
}  
  
.offset-3 {  
  margin-left: 25%;  
}  
  
.offset-4 {  
  margin-left: 33.33333333%;  
}  
  
.offset-5 {  
  margin-left: 41.66666667%;  
}  
  
.offset-6 {  
  margin-left: 50%;  
}  
  
.offset-7 {  
  margin-left: 58.33333333%;  
}  
  
.offset-8 {  
  margin-left: 66.66666667%;  
}  
  
.offset-9 {  
  margin-left: 75%;  
}  
  
.offset-10 {  
  margin-left: 83.33333333%;  
}  
  
.offset-11 {  
  margin-left: 91.66666667%;  
}  
  
.g-0,  
.gx-0 {  
  --bs-gutter-x: 0;  
}  
  
.g-0,  
.gy-0 {  
  --bs-gutter-y: 0;  
}  
  
.g-1,  
.gx-1 {  
  --bs-gutter-x: 0.25rem;  
}  
  
.g-1,  
.gy-1 {  
  --bs-gutter-y: 0.25rem;  
}  
  
.g-2,  
.gx-2 {  
  --bs-gutter-x: 0.5rem;  
}  
  
.g-2,  
.gy-2 {  
  --bs-gutter-y: 0.5rem;  
}  
  
.g-3,  
.gx-3 {  
  --bs-gutter-x: 1rem;  
}  
  
.g-3,  
.gy-3 {  
  --bs-gutter-y: 1rem;  
}  
  
.g-4,  
.gx-4 {  
  --bs-gutter-x: 1.5rem;  
}  
  
.g-4,  
.gy-4 {  
  --bs-gutter-y: 1.5rem;  
}  
  
.g-5,  
.gx-5 {  
  --bs-gutter-x: 3rem;  
}  
  
.g-5,  
.gy-5 {  
  --bs-gutter-y: 3rem;  
}  
  
@media (min-width: 576px) {  
  .col-sm {  
    flex: 1 0 0%;  
  }  
  .row-cols-sm-auto > * {  
    flex: 0 0 auto;  
    width: auto;  
  }  
  .row-cols-sm-1 > * {  
    flex: 0 0 auto;  
    width: 100%;  
  }
......
......
......
```


# 3. Other specifications

## 3.1 prefix

- Prefix all custom variables with labels to avoid conflicts.

```scss
$variable-prefix:             bs- !default;   
$prefix:                      $variable-prefix !default;
```

## 3.2 Gradient

-  The gradient which is added to components if `$enable-gradients` is `true`  
-  This gradient is also added to elements with `.bg-gradient`

```scss
$gradient: linear-gradient(180deg, rgba($white, .15), rgba($white, 0)) !default;
```

## 3.3 Spacing

```scss
$spacer: 1rem !default;  
$spacers: (  
  0: 0,  
  1: $spacer * .25,  
  2: $spacer * .5,  
  3: $spacer,  
  4: $spacer * 1.5,  
  5: $spacer * 3,  
) !default;
```

## 3.4 Position  

-  Define the edge positioning anchors of the position utilities.  

```scss
$position-values: (  
  0: 0,  
  50: 50%,  
  100: 100%  
) !default;
```

## 3.5 Body

-  Settings for the `<body>` element.

```scss
$body-text-align:           null !default;  
$body-color:                $gray-900 !default;  
$body-bg:                   $white !default;  
$body-secondary-color:      rgba($body-color, .75) !default;  
$body-secondary-bg:         $gray-200 !default;  
$body-tertiary-color:       rgba($body-color, .5) !default;  
$body-tertiary-bg:          $gray-100 !default;  
$body-emphasis-color:       $black !default;
```

## 3.6  Links

```scss
$link-color:                              $primary !default;  
$link-decoration:                         underline !default;  
$link-shade-percentage:                   20% !default;  
$link-hover-color:                        shift-color($link-color, $link-shade-percentage) !default;  
$link-hover-decoration:                   null !default;  
$stretched-link-pseudo-element:           after !default;  
$stretched-link-z-index:                  1 !default;
```

## 3.7 Icon links

```scss
$icon-link-gap:               .375rem !default;  
$icon-link-underline-offset:  .25em !default;  
$icon-link-icon-size:         1em !default;  
$icon-link-icon-transition:   .2s ease-in-out transform !default;  
$icon-link-icon-transform:    translate3d(.25em, 0, 0) !default;
```

## 3.8 Paragraphs

```scss
$paragraph-margin-bottom:   1rem !default;
```

## 3.9 Border

```scss
$border-width:                1px !default;  
$border-widths: (  
  1: 1px,  
  2: 2px,  
  3: 3px,  
  4: 4px,  
  5: 5px  
) !default;  
$border-style:                solid !default;  
$border-color:                $gray-300 !default;  
$border-color-translucent:    rgba($black, .175) !default;


$border-radius:               .375rem !default;  
$border-radius-sm:            .25rem !default;  
$border-radius-lg:            .5rem !default;  
$border-radius-xl:            1rem !default;  
$border-radius-xxl:           2rem !default;  
$border-radius-pill:          50rem !default;

$border-radius-2xl:           $border-radius-xxl !default; // Deprecated in v5.3.0
```

## 3.10 Box

```scss
$box-shadow:                  0 .5rem 1rem rgba($black, .15) !default;  
$box-shadow-sm:               0 .125rem .25rem rgba($black, .075) !default;  
$box-shadow-lg:               0 1rem 3rem rgba($black, .175) !default;  
$box-shadow-inset:            inset 0 1px 2px rgba($black, .075) !default;
```

## 3.11 Font

```scss
$font-size-root:              null !default;  
$font-size-base:              1rem !default; // Assumes the browser default, typically `16px`  
$font-size-sm:                $font-size-base * .875 !default;  
$font-size-lg:                $font-size-base * 1.25 !default;  
  
$font-weight-lighter:         lighter !default;  
$font-weight-light:           300 !default;  
$font-weight-normal:          400 !default;  
$font-weight-medium:          500 !default;  
$font-weight-semibold:        600 !default;  
$font-weight-bold:            700 !default;  
$font-weight-bolder:          bolder !default;  
  
$font-weight-base:            $font-weight-normal !default;  
  
$line-height-base:            1.5 !default;  
$line-height-sm:              1.25 !default;  
$line-height-lg:              2 !default;  
  
$h1-font-size:                $font-size-base * 2.5 !default;  
$h2-font-size:                $font-size-base * 2 !default;  
$h3-font-size:                $font-size-base * 1.75 !default;  
$h4-font-size:                $font-size-base * 1.5 !default;  
$h5-font-size:                $font-size-base * 1.25 !default;  
$h6-font-size:                $font-size-base !default;  
// scss-docs-end font-variables  
  
// scss-docs-start font-sizes  
$font-sizes: (  
  1: $h1-font-size,  
  2: $h2-font-size,  
  3: $h3-font-size,  
  4: $h4-font-size,  
  5: $h5-font-size,  
  6: $h6-font-size  
) !default;
```

```scss
$headings-margin-bottom:      $spacer * .5 !default;  
$headings-font-family:        null !default;  
$headings-font-style:         null !default;  
$headings-font-weight:        500 !default;  
$headings-line-height:        1.2 !default;  
$headings-color:              inherit !default;  
// scss-docs-end headings-variables  
  
// scss-docs-start display-headings  
$display-font-sizes: (  
  1: 5rem,  
  2: 4.5rem,  
  3: 4rem,  
  4: 3.5rem,  
  5: 3rem,  
  6: 2.5rem  
) !default;  
  
$display-font-family: null !default;  
$display-font-style:  null !default;  
$display-font-weight: 300 !default;  
$display-line-height: $headings-line-height !default;  
// scss-docs-end display-headings  
  
// scss-docs-start type-variables  
$lead-font-size:              $font-size-base * 1.25 !default;  
$lead-font-weight:            300 !default;  
  
$small-font-size:             .875em !default;  
  
$sub-sup-font-size:           .75em !default;  
  
// fusv-disable  
$text-muted:                  var(--#{$prefix}secondary-color) !default; // Deprecated in 5.3.0  
// fusv-enable  
  
$initialism-font-size:        $small-font-size !default;  
  
$blockquote-margin-y:         $spacer !default;  
$blockquote-font-size:        $font-size-base * 1.25 !default;  
$blockquote-footer-color:     $gray-600 !default;  
$blockquote-footer-font-size: $small-font-size !default;  
  
$hr-margin-y:                 $spacer !default;  
$hr-color:                    inherit !default;  
  
$hr-bg-color:                 null !default; // Deprecated in v5.2.0  
$hr-height:                   null !default; // Deprecated in v5.2.0  
  
$hr-border-color:             null !default; // Allows for inherited colors  
$hr-border-width:             var(--#{$prefix}border-width) !default;  
$hr-opacity:                  .25 !default;  
  
$vr-border-width:             var(--#{$prefix}border-width) !default;  
  
$legend-margin-bottom:        .5rem !default;  
$legend-font-size:            1.5rem !default;  
$legend-font-weight:          null !default;  
  
$dt-font-weight:              $font-weight-bold !default;  
  
$list-inline-padding:         .5rem !default;
```


## 3.12 Typography

```scss
// Font, line-height, and color for body text, headings, and more.  
  
// scss-docs-start font-variables  
// stylelint-disable value-keyword-case  
$font-family-sans-serif:      system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", "Noto Sans", "Liberation Sans", Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji" !default;  
$font-family-monospace:       SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace !default;  
// stylelint-enable value-keyword-case  
$font-family-base:            var(--#{$prefix}font-sans-serif) !default;  
$font-family-code:            var(--#{$prefix}font-monospace) !default;  
  
// $font-size-root affects the value of `rem`, which is used for as well font sizes, paddings, and margins  
// $font-size-base affects the font size of the body text  
$font-size-root:              null !default;  
$font-size-base:              1rem !default; // Assumes the browser default, typically `16px`  
$font-size-sm:                $font-size-base * .875 !default;  
$font-size-lg:                $font-size-base * 1.25 !default;  
  
$font-weight-lighter:         lighter !default;  
$font-weight-light:           300 !default;  
$font-weight-normal:          400 !default;  
$font-weight-medium:          500 !default;  
$font-weight-semibold:        600 !default;  
$font-weight-bold:            700 !default;  
$font-weight-bolder:          bolder !default;  
  
$font-weight-base:            $font-weight-normal !default;  
  
$line-height-base:            1.5 !default;  
$line-height-sm:              1.25 !default;  
$line-height-lg:              2 !default;  
  
$h1-font-size:                $font-size-base * 2.5 !default;  
$h2-font-size:                $font-size-base * 2 !default;  
$h3-font-size:                $font-size-base * 1.75 !default;  
$h4-font-size:                $font-size-base * 1.5 !default;  
$h5-font-size:                $font-size-base * 1.25 !default;  
$h6-font-size:                $font-size-base !default;  
// scss-docs-end font-variables  
  
// scss-docs-start font-sizes  
$font-sizes: (  
  1: $h1-font-size,  
  2: $h2-font-size,  
  3: $h3-font-size,  
  4: $h4-font-size,  
  5: $h5-font-size,  
  6: $h6-font-size  
) !default;  
// scss-docs-end font-sizes  
  
// scss-docs-start headings-variables  
$headings-margin-bottom:      $spacer * .5 !default;  
$headings-font-family:        null !default;  
$headings-font-style:         null !default;  
$headings-font-weight:        500 !default;  
$headings-line-height:        1.2 !default;  
$headings-color:              inherit !default;  
// scss-docs-end headings-variables  
  
// scss-docs-start display-headings  
$display-font-sizes: (  
  1: 5rem,  
  2: 4.5rem,  
  3: 4rem,  
  4: 3.5rem,  
  5: 3rem,  
  6: 2.5rem  
) !default;  
  
$display-font-family: null !default;  
$display-font-style:  null !default;  
$display-font-weight: 300 !default;  
$display-line-height: $headings-line-height !default;  
// scss-docs-end display-headings  
  
// scss-docs-start type-variables  
$lead-font-size:              $font-size-base * 1.25 !default;  
$lead-font-weight:            300 !default;  
  
$small-font-size:             .875em !default;  
  
$sub-sup-font-size:           .75em !default;  
  
// fusv-disable  
$text-muted:                  var(--#{$prefix}secondary-color) !default; // Deprecated in 5.3.0  
// fusv-enable  
  
$initialism-font-size:        $small-font-size !default;  
  
$blockquote-margin-y:         $spacer !default;  
$blockquote-font-size:        $font-size-base * 1.25 !default;  
$blockquote-footer-color:     $gray-600 !default;  
$blockquote-footer-font-size: $small-font-size !default;  
  
$hr-margin-y:                 $spacer !default;  
$hr-color:                    inherit !default;  
  
// fusv-disable  
$hr-bg-color:                 null !default; // Deprecated in v5.2.0  
$hr-height:                   null !default; // Deprecated in v5.2.0  
// fusv-enable  
  
$hr-border-color:             null !default; // Allows for inherited colors  
$hr-border-width:             var(--#{$prefix}border-width) !default;  
$hr-opacity:                  .25 !default;  
  
// scss-docs-start vr-variables  
$vr-border-width:             var(--#{$prefix}border-width) !default;  
// scss-docs-end vr-variables  
  
$legend-margin-bottom:        .5rem !default;  
$legend-font-size:            1.5rem !default;  
$legend-font-weight:          null !default;  
  
$dt-font-weight:              $font-weight-bold !default;  
  
$list-inline-padding:         .5rem !default;  
  
$mark-padding:                .1875em !default;  
$mark-color:                  $body-color !default;  
$mark-bg:                     $yellow-100 !default;
```

## 3.13 Others

- The rest includes components like table, form, input, dropdown, and so on.

# 4. Summary


### 1. Colors

- **Gray Scale**
- **Primary Colors**
    - primary
    - secondary
    - success
    - danger
    - warning
    - info
- **Secondary Colors**
    - light
    - dark
    - white
    - black
- **Background Colors**
    - background-color
    - text-color
    - border-color
    - background-opacity
    - background-image
    - background-image-size
    - background-position
- **Text Colors**
    - text-color
    - link-color
    - hover-color
    - active-color
    - disabled-color
    - text-shadow-color
    - text-shadow-size

### 2. Layout

- **Containers**
    - container-width
    - max-width
    - margin
    - padding
    - background-color
    - background-image
    - background-image-size
    - background-position
- **Grid System**
    - number-of-columns
    - column-width
    - column-gap
    - column-offset
    - column-alignment
    - background-color
    - background-image
    - background-image-size
    - background-position
- **Spacing**
    - margin-size
    - margin-unit
    - padding-size
    - padding-unit
    - border-color
    - padding-color

### 3. Typography

- **Font Family**
    - font-name
    - font-style
    - font-weight
    - font-size
    - font-scale
    - font-scale-size
- **Font Size**
    - font-size
    - line-height
    - font-scale
    - font-scale-size
    - font-scale-unit
- **Line Height**
    - line-height
    - text-align
    - text-indent
    - text-indent-size
    - text-indent-unit

### 4. Components

- **Alerts**
    - alert-color
    - alert-background-color
    - alert-border-color
    - alert-icon
- **Badges**
    - badge-color
    - badge-background-color
    - badge-border-color
- **Breadcrumbs**
    - breadcrumb-color
    - breadcrumb-background-color
    - breadcrumb-border-color
- **Buttons**
    - button-color
    - button-size
    - button-style
    - button-border-color
    - button-background-color
    - button-background-image
    - button-background-image-size
    - button-background-position
- **Cards**
    - card-color
    - card-background-color
    - card-border-color
    - card-image
    - card-image-size
    - card-image-position
- **Carousels**
    - carousel-color
    - carousel-background-color
    - carousel-border-color
    - carousel-image
    - carousel-image-size
    - carousel-image-position
- **Collapse**
    - collapse-color
    - collapse-background-color
    - collapse-border-color
- **Dropdowns**
    - dropdown-color
    - dropdown-background-color
    - dropdown-border-color
    - dropdown-caret-color
- **Forms**
    - form-element-size
    - form-element-style
    - form-element-border-color
    - form-element-background-color
    - form-element-background-image
    - form-element-background-image-size
    - form-element-background-position
    - input-color
    - input-background-color
    - input-border-color
    - input-placeholder-color
- **Input Groups**
    - input-group-color
    - input-group-background-color
    - input-group-border-color
- **Jumbotrons**
    - jumbotron-color
    - jumbotron-background-color
    - jumbotron-border-color
- **List Groups**
    - list-group-color
    - list-group-background-color
    - list-group-border-color
- **Media Objects**
    - media-object-color
    - media-object-background-color
    - media-object-border-color
- **Modals**
    - modal-color
    - modal-background-color
    - modal-border-color
    - modal-header-color
    - modal-header-background-color
    - modal-header-border-color
    - modal-body-color
    - modal-body-background-color
    - modal-body-border-color
    - modal-footer-color
    - modal-footer-background-color
    - modal-footer-border-color
- **Navbars**
    - navbar-color
    - navbar-background-color
    - navbar-border-color
    - navbar-brand-color
    - navbar-brand-background-color
    - navbar-brand-border-color
- **Navigation**
    - navigation-style
    - navigation-size
    - navigation-border-color
    - navigation-background-color
    - navigation-background-image
    - navigation-background-image-size
    - navigation-background-position
- **Pagination**
    - pagination-color
    - pagination-background-color
    - pagination-border-color
- **Popovers**
    - popover-color
    - popover-background-color
    - popover-border-color
- **Progress Bars**
    - progress-bar-color
    - progress-bar-background-color
    - progress-bar-border-color
    - progress-bar-striped
- **Scrollspy**
    - scrollspy-color
    - scrollspy-background-color
    - scrollspy-border-color
- **Tables**
    - table-color
    - table-background-color
    - table-border-color
    - table-striped
    - table-hover
    - table-condensed
- **Tabs**
    - tab-color
    - tab-background-color
    - tab-border-color
    - tab-active-color
    - tab-active-background-color
    - tab-active-border-color
- **Tooltips**
    - tooltip-color
    - tooltip-background-color
    - tooltip-border-color
    - tooltip-arrow-color
- **Typography**
    - font-family
    - font-size
    - font-weight
    - line-height
    - text-align
    - text-indent
    - text-transform
- **Utilities**
    - border-radius
    - box-shadow
    - opacity
    - overflow
    - padding
    - margin
    - width
    - height
    - z-index

### 5. Borders

- **Border Style**
    - border-width
    - border-style
    - border-color
    - border-opacity
    - shadow-color
    - shadow-size
- **Border Color**
    - border-color
    - border-opacity
    - shadow-color
    - shadow-size

### 6. Animations

- **Animation Duration**
    - animation-duration
    - animation-delay
    - animation-speed
    - animation-direction
- **Animation Style**
    - animation-style
    - animation-direction
    - animation-speed
    - animation-delay

### 7. Misc

- **Shadows**
    - shadow-size
    - shadow-color
    - shadow-opacity
    - shadow-direction
    - shadow-offset
- **Transitions**
    - transition-duration
    - transition-delay
    - transition-speed
    - transition-direction
- **Z-Index**
    - z-index
    