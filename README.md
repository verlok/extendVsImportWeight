# `@extend` vs `@include` weight

Compares the final CSS weight when using extend vs include, one rule vs many rules

## What it does

This repo compares extend vs import, in both cases: single CSS rule and many CSS rules

* Using `@extend` of a single CSS rule --> `extendSingleRule.scss`
* Using `@extend` of few CSS rules --> `extendFewRules.scss`
* Using `@extend` of many CSS rules --> `extendManyRules.scss`
* Using `@include` of a single CSS rule mixin --> `includeSingleRule.scss`
* Using `@include` of a few CSS rules mixin --> `includeFewRules.scss`
* Using `@include` of a many CSS rules mixin --> `includeManyRules.scss`

### `extendSingleRule.scss`

```SCSS
%floatMeLeft {
	float: left;
}

.one {
	@extend %floatMeLeft;
}

// ...

.onehundred {
	@extend %floatMeLeft;
}
```

### `extendFewRules.scss`

```SCSS
%microClearfix {
	&:before,
	&:after {
		content: " ";
		display: table;
	}

	&:after {
		clear: both;
	}
}

.one {
	@extend %microClearfix;
}

// ...

.onehundred {
	@extend %floatMeLeft;
}
```


### `extendManyRules.scss`

```SCSS
%myButton {
	background-color: black;
	color: white;
	padding: 1em;
	margin: 0;
	display: block;
	border-radius: 2px;
	text-shadow: 0 0 2px rgba(0,0,0,.8);
	box-shadow: 0 0 2px rgba(0,0,0,.2);
	&:hover {
        color: black;
        background-color: white;
    }
}

.one {
	@extend %myButton;
}

// ...

.onehundred {
	@extend %myButton;
}
```

### `includeSingleRule.scss`

```SCSS
@mixin floatMeLeft {
	float: left;
}

.one {
	@include floatMeLeft;
}

// ...

.onehundred {
	@include floatMeLeft;
}
```

### `includeFewRules.scss`

```SCSS
@mixin microClearfix {
	&:before,
	&:after {
		content: " ";
		display: table;
	}

	&:after {
		clear: both;
	}
}

.one {
	@include microClearfix;
}

// ...

.onehundred {
	@include microClearfix;
}
```

### `includeManyRules.scss`

```SCSS
@mixin myButton {
	background-color: black;
	color: white;
	padding: 1em;
	margin: 0;
	display: block;
	border-radius: 2px;
	text-shadow: 0 0 2px rgba(0,0,0,.8);
	box-shadow: 0 0 2px rgba(0,0,0,.2);
	&:hover {
	    color: black;
	    background-color: white;
	}
}

.one {
	@include myButton;
}

// ...

.onehundred {
	@include myButton;
}
```

## What is the result

### Single rule

* `extendSingleRule.css` --> 1.182 bytes (360 bytes after GZip)
* `includeSingleRule.css` --> 3.072 bytes (408 bytes bytes after GZip)

### Few rules

* `extendFewRules.css` --> 5.427 bytes (669 bytes after GZip)
* `includeFewRules.css` --> 10.720 bytes (1.199 bytes after GZip)

### Many rules

* `extendManyRules.css` --> 3.152 bytes (759 bytes after GZip)
* `includeManyRules.css` --> 25.946 bytes (1.015 bytes after GZip)


## Conclusion

#### Before GZip


* Using `@include` for a single rule generates a **2 times bigger** CSS file, compared to `@extend`
* Using `@include` for a few rules generates a **2 times bigger** CSS file, compared to `@extend`
* Using `@include` for many rules generates a **8 times bigger** CSS file, compared to `@extend`


#### After GZip compression

* Using `@include` for a single rule generates a **1.13 times bigger** file, compared to `@extend`
* Using `@include` for a few rules generates a **1.79 times bigger** file, compared to `@extend`
* Using `@include` for many rules generates a **1.33 times bigger** file, compared to `@extend`


## What should front-end developers do

Due to [`@extend` limits with media queries](http://css-tricks.com/the-extend-concept/), using `@import` can be easier, BUT when using `@import` you should consider file weight and browser computing time.

If you need to propagate single CSS rules or few of them, @import might be a good way to go.
If you need to propagate many CSS rules, you should consider @extend and [watch out for media queries](http://css-tricks.com/the-extend-concept/).