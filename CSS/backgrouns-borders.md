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