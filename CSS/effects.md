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

