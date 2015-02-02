# `@extend` vs `@include` weight

Compares the final CSS weight when using extend vs include, one rule vs many rules

## What it does

This repo just compares extend vs import, in both cases: single CSS rule and many CSS rules

* Using `@extend` of a single CSS rule mixin --> `extendOneRule.scss`
* Using `@extend` of a multiple CSS rules mixin --> `extendMultipleRules.scss`
* Using `@include` of a single CSS rule mixin --> `includeOneRule.scss`
* Using `@include` of a multiple CSS rules mixin --> `includeMultipleRules.scss`

## What is the result

### CSS file size

#### Multiple rules

* `extendMultipleRules.css` --> 1.350 bytes
* `includeMultipleRules.css` --> 19.872 bytes

#### Single rule

* `extendOneRule.css` --> 1.182 bytes
* `includeOneRule.css` --> 3.072 bytes

### CSS file size after GZip

#### Multiple rules

* `extendMultipleRules.css.gz` --> 462 bytes
* `includeMultipleRules.css.gz` --> 595 bytes

#### Single rule

* `extendOneRule.css.gz` --> 357 bytes
* `includeOneRule.css.gz` --> 405 bytes

## Conclusion

#### Before GZip

* Using `@include` for many rules generates a **15 times bigger** CSS file, compared to `@extend`
* Using `@include` for a single rule generates a **2 times bigger** CSS file, compared to `@extend`

#### After GZip compression

* Using `@include` for many rules generates a **1.29 times bigger** file, compared to `@extend`
* Using `@include` for a single rule generates a **1.13 times bigger** file, compared to `@extend`

## What front-end developers do

Due to [`@extend` limits with media queries](http://css-tricks.com/the-extend-concept/), using `@import` can be easier, BUT when using `@import` you should consider file weight and browser computing time.

If you need to propagate single CSS rules or few of them, @import might be a good way to go.
If you need to propagate many CSS rules, you should consider @extend and [watch out for media queries](http://css-tricks.com/the-extend-concept/).