# extendVsIncludeWeight

Compares the final CSS weight when using extend vs include, one rule vs many rules

## What it does

This repo just compares extend vs import, in both cases: single CSS rule and many CSS rules

* Using `@extend` of a single CSS rule mixin --> `extendOneRule.scss`
* Using `@extend` of a multiple CSS rules mixin --> `extendMultipleRules.scss`
* Using `@include` of a single CSS rule mixin --> `includeOneRule.scss`
* Using `@include` of a multiple CSS rules mixin --> `includeMultipleRules.scss`

## What is the result

### CSS file size

* `extendOneRule.css` --> 112 bytes
* `extendMultipleRules.css` --> 280 bytes
* `includeOneRule.css` --> 321 bytes 
* `includeMultipleRules.css` --> 2.337 bytes

### CSS file size after GZip

* `extendOneRule.css.gz` --> 124 bytes
* `extendMultipleRules.css.gz` --> 216 bytes
* `includeOneRule.css.gz` --> 133 bytes 
* `includeMultipleRules.css.gz` --> 239 bytes
