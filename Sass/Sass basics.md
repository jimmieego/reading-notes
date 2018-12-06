# Sass basics

[Source](https://sass-lang.com/guide)

## Variables

Sass use the `$` symbol to define a variable. Example:

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## Nesting

Sass will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. Be aware that overly nested rules will result in over-qualified CSS that could prove hard to maintain and is generally considered bad practice.

## Partials

A partial is simply a Sass file named with a leading underscore (e.g., `_partial.scss`). The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@import` directive.

## Import

Example:

```scss
// _reset.scss

html, body, ul, ol {
    margin: 0;
    padding: 0;
}
```

```scss
// base.scss

@import `reset`;

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

No need to include the file extension `.scss`.

## Mixins

A mixin lets you make groups of CSS declarations that you want to reuse throughout your site. You can even pass in values to make your mixin more flexible. 

A good use of a mixin is for vendor prefixes. Example:

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.box { @include transform(rotate(30deg)); }
```

## Extend/Inheritance

Using `@extend` lets you share a set of CSS properties from one selector to another.

```scss
/* Placeholder class. This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// Placeholder class. This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}

```

You can extend most simple CSS selectors in addition to placeholder classes in Sass, but using placeholders is the easiest way to make sure you aren't extending a class that's nested elsewhere in your styles, which can result in unintended selectors in your CSS.

## Operators

Sass has a handful of standard math operators like `+`, `-`, `*`, `/`, and `%`.

```scss
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```