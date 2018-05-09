# Values and Sizing

## Relative length units

In CSS 2.1:

- `em`: calculated from the `font-size` property of an element
- `ex`: calculated from the x-height of the element’s font

### Root-relative units

`rem`: relative to the `font-size` value of the document root (the `html` element). This is helpful for nested elements.

### Viewport-relative units

Percentage values are useful for layout elements at the top level, but you can run into difficulties when using percentages with nested elements.

- `vh`: viewport height
- `vw`: viewport width
- `vmax`: equilvalent to whichever is the greater value of `vh` and `vw`
- `vmin`: equilvalent to the lesser value

Each unit of value represents 1 percent of the appropriate viewport dimension.

Example:

```css
div {
    height: 50vh; /* 50% of viewport hight */
    width: 75vw; /* 75% of viewport width */
}

.container {
    width: 100vmax;
}
```

The advantage of using `vh` and `vw` is that when elements are nested, the units remain relative to the viewport. The utility of `vmax` and `vmin` is in ensuring an element remains proportional to the viewport regardless of orientation.

## Calculated values

CSS calculations are performed with the `calc()` function. It takes as an argument of any mathematical expression using common value units and four basic operands:

- `+` (addition),
- `-` (subtraction),
- `*` (multiplication),
- `/` (division).

The `calc()` is especially useful when mixing units. Example:

```css
div {
    border: 10px;
    width: calc(75% - 2em);
}
```

Note: must insert a single whitespace character around the operand.

## Sizing elements

### Box sizing

Syntax:

```css
div {
    box-sizing: keyword;
}
```

The `keyword` can be:

- `content-box`: default, which means apply the specified `width` or `height` to the content box only, as in the W3C model.
- `border-box`: any specified length should also include any padding and border boxes.

### Intrinsic and extrinsic sizing

*Intrinsic sizing* is based on an element’s *children*, and *extrinsic sizing* is based on the size of the *parent* element.

All of the intrinsic and extrinsic sizing models are applied using a keyword value on the `width` or `height` properties (and their `min-` and `max-` variants):

```css
div {
    width: keyword;
}
```

The `keyword` can be:

- `max-content`, `min-content`: intrinsic values that make an element as wide or as high as the largest (`max-content`) or smallest (`min-content`) item of content it contains.
- `fit-content`: the element will expand to be just wide enough to contain its content, unless the maximum width of the element is reached, in which case, the content will wrap.