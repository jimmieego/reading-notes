# Color

## The `opacity` property

The `opacity` property is the measure of the opacity of an *element*.

```css
div {
	opacity: 0.5; /* a number between 0.0 and 1.0 */
	/*
	0 is fully transparent
	1 is fully opaque
	*/
}
```

**Note**:

- Opacity affects not only the element it’s applied to but also all of that element’s children. You can never make an element more opaque than its parent, but you can make it *less* opaque.
- Set a low `opacity` value to dim hyperlinked images in your designs and set a higher `opacity` value to brighten them up when hovered or focused.

## New and extended color values

### The alpha channel

The *Alpha channel* is the measure of the opacity of a *color*. 

The `rgba()` function:

```css
E { color: rgba(red, green, blue, alpha); } /* alpha is a decimal fraction from 0.0 to 1.0 */
```

Note:
- `rgba()` is a color value, so you couldn’t, for example, use it to change the opacity of an image (or an element with a background image).
- although the value of the `rgba()` function can be inherited, child elements can overrule with an `rgba()` value of their own.
- Specify solid backups for RGBA colors in a separate rule that appears *before* the RGBA rule.

### HSL color

The `hsl()` function:

```css
E { color: hsl(hue,saturation,lightness); }
```

- `hue`: number between 0 and 360
- `saturation`: 0% to 100%. 0 percent is zero intensity, which makes the color a shade of gray, and 100 percent is full strength, the most intense version of that color.
- `lightness`: 0% to 100%. 50 percent is the true color, 0 percent is black, and 100 percent is white.

The `hsla()` adds the alpha channel.

### The color variable: `currentColor`

The value of `currentColor` for an element is the value of its own `color` property. You can update the parent element color and not have to worry about setting the color on any relevant children.