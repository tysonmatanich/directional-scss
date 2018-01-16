# Directional-SCSS

Makes supporting both left-to-right (LTR) and right-to-left (RTL) easy. By including `directional.scss` into your project and using its Sass variables, functions, and mixins, you can create an LTR and RTL CSS bundle for your site.

* Author: Tyson Matanich - http://matanich.com
* License: MIT

**Article:** http://www.matanich.com/2013/09/06/rtl-css-with-sass/

**Demos:**
* RTL - http://codepen.io/tysonmatanich/pen/GnKhA
* LTR - http://codepen.io/tysonmatanich/pen/mCavA

## Features

### Variables
* `$dir` - defaults to **ltr** but can be set to **rtl**
* `$left` - set to **left** when `$dir` equals **ltr** and **right** when `$dir` equals **rtl**
* `$right` - set to **right** when `$dir` equals **ltr** and **left** when `$dir` equals **rtl**

### Functions
* `if-ltr($if)` - returns `$if` param when `$dir` equals **ltr** otherwise returns nothing
* `if-ltr($if, $else)` - returns `$if` param when `$dir` equals **ltr** otherwise returns `$else` param
* `if-rtl($if)` - returns `$if` param when `$dir` equals **rtl** otherwise returns nothing
* `if-rtl($if, $else)` - returns `$if` param when `$dir` equals **rtl** otherwise returns `$else` param
* `side-values($values)` - switches the left and right values of the `$values` list when `$dir` equals **rtl**
* `corner-values($values)` - switches the left and right values of the `$values` list when `$dir` equals **rtl**

### Mixins
* `@include if-ltr { /*content*/ }` - returns the `@content` when `$dir` equals **ltr** otherwise returns nothing
* `@include if-rtl { /*content*/ }` - returns the `@content` when `$dir` equals **rtl** otherwise returns nothing

## Example
```scss
// Import helpers from directional.scss
@import "directional";

// Use the helpers enable creating CSS bundles for LTR and RTL
body {
    text-align: $left;
}

p {
    padding-#{$right}: 1em;
    margin: side-values(0 2em 0 1em) if-ltr(!important);
    background-image: url(sprite#{if-rtl('-rtl')}.png);

    &:before {
        content: if-ltr('<', '>');
    }

    &:after {
        content: if-rtl('>', '<');
    }

    @include if-ltr {
        strong {
            padding-left: 0.5em;
        }
    }

    @include if-rtl {
        em {
            margin-right: 0.5em;
        }
    }
}

.icon.icon-star {
    background-image: url(sprite-#{$dir}.png);
}
```

To bring it all together your project should look something like the following:

**site-ltr.scss**
```scss
@import 'site.scss';
```

**site-rtl.scss** (overrides $dir)
```scss
$dir: rtl;
@import 'site.scss';
```

**site.scss**
```scss
@import 'directional.scss';

// Your site styles here using directional-scss variables, functions, and mixins
```

Then reference the appropriate bundle (site-ltr.css or site-rtl.css) needed for the current page:
```html
<!DOCTYPE html>
<html>
<head>
    <link href="/site-ltr.css" rel="stylesheet"/>
</head>
<body>
</body>
</html>
```
