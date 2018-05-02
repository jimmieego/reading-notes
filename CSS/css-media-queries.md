# CSS Media Queries

## Syntax

Declaration methods:

```html
<link href="file" rel="stylesheet" media="logic media and (expression)">
```

```css
@import url('file') logic media and (expression);
```

```
@media logic media and (expression) {
	rules
}
```

The most common `media` type values are `screen` and `print`. The `logic` can be either `only` or `not`. 

## `Width` and `Height`

`width` and `height` can also have `max-` and `min-` prefixes. They are measured in CSS pixels.

Example:

```css
@media (min-width: 400px) {
    h1 { 
    	background: url('landscape.jpg'); 
    }
}
```

## Pixel Ratio

`resolution`: The value of `resolution` is a number with a unit of resolution: *dots per inch (DPI)*, *dots per centimeter (DPCM)*, or *dots per pixel (DPPX)*. 

You can also have `max-resolution` and `min-resolution`.

Example:

```css
#element { 
	background-image: url('image-lores.png'); 
}

􏰁@media (min-resolution: 1.5dppx) {
	#element {
		background-image: url('image-hires.png'); 􏰂 
		background-size: 100% 100%;
	}
}
```

## Mobile First

The mobile-first way to create your pages is to first make a basic style sheet, which is applied to all browsers, including mobile, and to then progressively add assets and features for users with larger screens, loaded using a media query with the `min-width` feature.