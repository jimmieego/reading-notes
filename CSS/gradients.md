# Gradients

**Note**: Graphical effects like gradients can be quite computationally taxing and will slow the rendering and performance of pages, especially in mobile browsers.

## Linear gradients

Example:

```css
div {
	background-image: linear-gradient(black, white);
}
```

`linear-gradient()` takes a comma-separated list of *color-stops*.

### Setting gradient direction

```css
div {
	background-image: linear-gradient(to top, black, white);
}

.foo {
	background-image: linear-gradient(to right bottom, black, white); /*top-left to bottom-right*/
}

.foo2 {
	background-image: linear-gradient(135deg, black, white); /* top-left to bottom-right*/
}
```

The default direction is from top to bottom vertically.

### Adding extra color-stop values

```css
div {
	background-image: linear-gradient(black, white 75%, black);
	/* positions the white color-stop at 75 percent of the length of the gradient line */
}
```

### Repeating linear gradients

```css
div {
	background-image: repeating-linear-gradient(white, black 25%);
}
```

A length or percentage value is required for the final color-stop. The final color-stop value sets the point at which the gradient should end and then start repeating.

## Radial gradients

Example:

```css
div {
	background-image: radial-gradient(white, black);
}
```

### Shape

You can set the shape of a radial gradient by adding a keyword before the color-stops. The default is `ellipse`, but you can use the alternative `circle`:

```css
div {
	background-image: radial-gradient(circle at 100% 50%, white, black);
} 
```

The default center of a radial gradient is at the center of the element. You can set the gradient center position after the shape keyword.

### Extent

You can also set the *extent* of a gradient:

```css
div {
	background-image: radial-gradient(circle 50px, black, white);
	/*The extent argument is placed immediately after the shape keyword*/
}
```

The *extent* can be a length or position value or one of four extent keywords: 

- `closest-corner`
- `closest-side`
- `farthest-corner` (the default)
- `farthest-side`

### Using multiple color-stop values

Radial gradients can accept multiple color-stop values and length or percentage values for positioning control. 

Example:

```css
.gradient-3 { 
	background-image: radial-gradient(farthest-side circle at left, white, black 25%, white 75%, black);
}
```

### Repeating radial gradients

Example:

```css
div {
	background-image: repeating-radial-gradient(circle, black, white 20%);
	/* a circular gradient, repeats black-white every 20 percent until its extent is reached */
}
```

## Multiple gradients

Because gradients are applied with the `background-image` property, you can use CSS3’s multiple background values’ syntax to apply multiple gradients to an element using comma-separated values.

Examples:

```css
.linears {
  background-image:
  linear-gradient(to right bottom, black, white 50%, transparent 50%),
  linear-gradient(to left bottom, black, white 50%, black 50%);
}
.radials {
  background-image:
  radial-gradient(closest-side circle at 20% 50%, white, black 95%, transparent),
  radial-gradient(closest-side circle at 50% 50%, white, black 95%, transparent),
  radial-gradient(closest-side circle at 80% 50%, white, black 95%, transparent);
}

/* the last color-stop has a value of transparent to allow the layers below to show through. */
```