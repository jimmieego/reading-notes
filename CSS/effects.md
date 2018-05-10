# Blend modes, filter effects, masking

These non-destructive effects only alter the way images are displayed on the page; they don’t modify the source images.

## Blend modes

Blend modes are a way to mix an image into a solid color or another image so the two appear merged or blended.

- *Screen*: In this mode, whites remain white, whereas black lets the back- ground color show through. As a result of applying this mode, images tend to become lighter.
- *Multiply*: This mode tends to produce darker images. Blacks remain black, whereas whites let the background color pass through.
- *Overlay*: The Overlay mode strikes a balance between the Screen and Multiply modes, useful when blending two images. Highlights and shadows are preserved, increasing contrast.

### `background-blend-mode`

Blends the background layers of an element (e.g., blend the background color with the background image). Only the background layers are blended; the element itself doesn’t blend with any part of the page below it.

Example:

```css
/* Blending an Image and a Color */
div {
    background: url('foo.png') #f00;
    background-blend-mode: multiply; /* the default is normal */
}

/* Blending Two Images */
div {
    background-color: transparent;
    background-image: url('foo.png'), url('bar.png'); background-blend-mode: multiply;
}

/* Multiple Blend Modes */
div {
    background-color: #f00;
    background-image: url('foo.png'), url('bar.png'); background-blend-mode: multiply, screen;
    /*
        Multiply mode will be used to blend the background color with foo.png; the result will be blended with bar.png using the Screen blend mode.
    */
}
```

### `mix-blend-mode`

Blends the content of the element with the content and background of any elements that are directly behind it on the screen.

Example:

```css
E { background-image: url('foo.png'); }
F { mix-blend-mode: multiply; }
```

### Isolation

Syntax:

```css
E {
    isolation: isolation-mode;
}
```

Makes an element create a new stacking context, similar to the way setting `position: relative` on an element resets the coordinates for absolute positioning.

The default value is `auto`. To create the new stacking context, use `isolate`:

```css
div { isolation: isolate; }
```

## Filter effects

Filters are used to change an element’s appearance before it reaches the page.

Syntax:

```css
E { filter: function; }
```

The `function` value is at least one of a range of nine filter effect functions. Each accepts a single argument, except when a series of arguments is required (in a space-separated list).

### `blur()`

Applies a blur effect to an element. The argument for the `blur()` function is a unit of length that controls the radius of the blur. The effect is called *Gaussian blur*. The higher the radius value, the greater the blur effect.

Example:

```css
E { filter: blur(10px); }
```

### `brightness()` and `contrast()`

The `brightness()` function changes the brightness of an element. The `contrast()` function increases or decreases the contrast between the dark and light of an element. Both functions take a percentage as an argument.

Example:

```css
E { filter: brightness(50%); }
E { filter: contrast(50%); }
```

Note:

- An argument of 100% leaves the element unchanged.
- An argument of 0% for `brightness()` makes the element fully black, and 0% for `contrast()` makes the element fully gray.

### `grayscale()`, `sepia()`, and `saturate()`

The `grayscale()` function replaces colors with shades of gray so you can convert images to black and white.

The `sepia()` toning function is similar to `grayscale()`, except it uses a gold tint to produce a vintage photo effect.

The `saturate()` function controls the color intensity.

All three functions accepts a percentage value as an argument:

```css
E { filter: grayscale(100%); } /* 100%: completely black and white */
E { filter: sepia(100%); } /* 100%: fully sepia toned */
E { filter: saturate(200%); }
```

Note: 

- A value of 0% for `grayscale()` and `sepia()` leaves the image unchanged.
- A value of 0% for `saturate()` makes an image appear fully unsaturated or grayscal; values greater than 100% oversaturate the image.

### `hue-rotate()`

Shifts the hue of all colors in an element around the color wheel by the same amount. The required argument is a degree:

```css
E { filter: hue-rotate(45deg); }
```

### `opacity()`

Works the same as the `opacity` property. The function accepts a percentage value as an argument, with 0% equal to fully transparent and 100% equal to fully opaque:

```css
E { filter: opacity(25%); }
```

### `drop-shadow()`

Syntax:

```css
E { filter: drop-shadow(5px 5px 3px gray); } /* x-offset, y-offset, blur radius, and shadow color */
```

The `drop-shadow()` function is aware of any alpha value (opacity) in the target element. The `box-shadow` property doesn’t care about alpha transparency, and its shadow follows only the outline of the element box.

### Multiple filter effect functions

List multiple filter functions in a space-separated list. Example:

```css
E { filter: blur(5px) drop-shadow(5px 5px 3px gray); }
```

Note:

- The order of the function is the order in which they'll be applied.
- When you list multiple functions in the `filter` property, any functions not in the list will have their values returned to the default.

### Filters in SVG

You can create your own filters in SVG and apply them in CSS by using an ID reference:

```svg
<filter id="blur">
    <feGaussianBlur stdDeviation="blur-radius" />
</filter>
```

Refer the SVG filter in CSS using the `url()`:

```css
E { filter: url('#blur'); } /* if the SVG is in line */
E { filter: url('filters.svg#blur'); } /* if the SVG is an external file */
```

Note this technique only works for a single filter.

## Masking

