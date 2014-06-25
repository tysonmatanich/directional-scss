# Directional-SCSS

Makes supporting both left-to-right (LTR) and right-to-left (RTL) easy.

* Author: Tyson Matanich - http://matanich.com
* License: MIT

**Article:** http://www.matanich.com/2013/09/06/rtl-css-with-sass/

**Demos:**
* RTL - http://codepen.io/tysonmatanich/pen/GnKhA
* LTR - http://codepen.io/tysonmatanich/pen/mCavA

##Features

###Variables
* `$dir` - defaults to **ltr** but can be set to **rtl**
* `$left` - set to **left** when `$dir` equals **ltr** and **right** when `$dir` equals **rtl**
* `$right` - set to **right** when `$dir` equals **ltr** and **left** when `$dir` equals **rtl**

###Functions
* `if-ltr($if)` - returns `$if` param when `$dir` equals **ltr** otherwise returns nothing
* `if-ltr($if, $else)` - returns `$if` param when `$dir` equals **ltr** otherwise returns `$else` param
* `if-rtl($if)` - returns `$if` param when `$dir` equals **rtl** otherwise returns nothing
* `if-rtl($if, $else)` - returns `$if` param when `$dir` equals **rtl** otherwise returns `$else` param
* `side-values($values)` - switches the left and right values of the `$values` list when `$dir` equals **rtl**
* `corner-values($values)` - switches the left and right values of the `$values` list when `$dir` equals **rtl**

###Mixins
* `@include if-ltr { /*content*/ }` - returns the `@content` when `$dir` equals **ltr** otherwise returns nothing
* `@include if-rtl { /*content*/ }` - returns the `@content` when `$dir` equals **rtl** otherwise returns nothing

##Example
```scss
// Override default value for $dir in directional.scss
$dir: rtl;

// Import helpers from directional.scss
@import "directional";

// Use the helpers to make CSS for LTR or RTL
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
