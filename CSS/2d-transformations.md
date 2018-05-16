# 2D Transformations

## The `transform` property

Basic syntax:

```css
E { transform: function(value); }
E { transform: function(value) function(value); }
```

### `rotate`

Example:

```css
div {
	transform: rotate(-15deg);
}
```

### Position in document flow

Transformed elements only affect rendering of the page, not document layout. The transformed element can cover subsequent elements.

### `transform-origin`

The *origin* of a transformation is the point on an element about which that transformation happens. The default point of origin in the CSS `transform` property is the element’s horizontal and vertical center. You can change it using:

```css
div {
	transform-origin: left top; /* horizontal, vertical; either one or two length, percentage, or keyword values */
}
```

### translate

`translate` moves the element from its default position along the horizontal or vertical axes. Movement along the horizontal axis is controlled with the `translateX()` function and along the vertical axis with `translateY()`:

```css
div {
	transform: translateX(20px) translateY(15%);
}
```

The shorthand function is `translate()`:

```css
div {
	transform: translate(20px, 15%);
}
```

### scale

Example:

```css
div {
	transform: scaleX(2) scaleY(3); /* unitless number as size ratio; default is 1 */
}
```

Shorthand function is `scale()`:

```css
div {
	transform: scale(2, 3);
}
```

Using a negative value has the effect of flipping the element, creating a “reflection” of the original element.

### skew

To *skew* an element is to alter the angle of its horizontal or vertical axis (or both axes).

Example:

```css
div {
	transform: skewX(15deg) skewY(-15deg);
	/*
	this is equilvant to rotate(15deg);
	*/
}
```

### Note

When you set the value of the `transform` property, any functions that you don’t list will be presumed to be reset to their default values. 