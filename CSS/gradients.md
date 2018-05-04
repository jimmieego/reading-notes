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