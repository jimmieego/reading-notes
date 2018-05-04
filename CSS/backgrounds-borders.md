## background-position

You can use key-words to specify a side and then length or percentage values for relative distance from that side.

```css
.foo { background-position: right 10em bottom 50%; }
```

## background-repeat

```css
.space { background-repeat: space; }
.round { background-repeat: round; }
```

`space` sets the background image to repeat across its containing element as many times as possible without clipping the image.

`round` sets the background image to repeat as many times as possible without clipping, but instead of equally spacing the repetitions, the images scales so a whole number of images fills the containing element.

```css
.foo { background-repeat: round space; }
```

The first value controls tiling on the horizontal axis, the second on the vertical.

## Multiple background images

Example:

```css
h2 {
    background-image: url('monkey.svg'), url('landscape.jpg');
    background-position: 95% 85%, 50% 50%;
    background-repeat: no-repeat;
}
```

or you can use the `background` shorthand property:

```css
h2 {
    background:
    url('monkey.svg') no-repeat 95% 85%,
    url('landscape.jpg') no-repeat 50% 50%;
}
```

Note the layers are created in reverse order: the first layer in the list becomes the topmost layer and so on.

## background-size

```css
div {
	background-size: 100px 200px; /* width height */
}
```

To make the image appear at its natual size, use `auto`. If you only specify a single value, that value is considered the `width`, and the height is then assigned the default value of `auto`.

`background-size` can also be set to:

- `contain`: sets the image to scale (proportionately) as large as possible, without exceeding either the height or width of the containing element.
- `cover`: sets the image to scale to the size of either the height or width of the containing element, whichever is larger.

## Background clip and origin

`background-clip` can be set to:

- `border-box`: the default; displays the background behind the border.
- `padding-box`: displays the background only up to, and not behind, the border.
- `content-box`: the background stops at the ele- ment’s padding.

`background-origin` sets the point where the background is calcuated to begin. It can be set to:

- `border-box`: the background originates at the limit of the border.
- `padding-box`: the background originates from the limit of the padding.
- `content-box`: the background originates from the limit of the content box.

## Borders with rounded corners

Example:

```css
div {
	border-top-left-radius: 10px 20px; /*irregular rounded corners*/
	border-top-right-radius: 20px; /*regular rounded corners*/
	border-bottom-right-radius: 20px;
	border-bottom-left-radius: 20px;
}
```

Shorthand property:

```css
div { border-radius: 20px 20px 10px 10px; } /*[top-left] [top-right] [bottom-right] [bottom-left]*/
```

Shorthand syntax with irregular curves:

```css
.radius-1 { border-radius: 20px / 10px; } /*horizontal-radius / vertical-radius*/
```

