# The New CSS Layout

Rachel Andrew

## Where we are

### CSS architecture

- [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
- [SMACSS](https://smacss.com/)
- [BEM](http://getbem.com/)

### Pre- and postprocessors

- [Sass](http://sass-lang.com/)
- [LESS](http://lesscss.org/)
- [Autoprefixer](https://github.com/postcss/autoprefixer)

### Component-first design

- [Atomic design](http://atomicdesign.bradfrost.com/)
- [Pattern Lab](https://patternlab.io/)
- [Fractal](https://fractal.build/)
- [Website Style Guide Resources](http://styleguides.io/)

## The new layout

### Formatting contexts in CSS

#### Block Formatting Context (BFC)

A new BFC is created any time an element:

- is the root element;
- is floated;
- has `position: absolute`, or
- has `display: inline-block`.

A new BFC is also created if the `overflow` property has a value other than `visible`.

Flex items, Grid items, and table cells also establish a new BFC for their child elements.

### Positioning

#### Relative positioning and absolute positioning

The item with `position: relative` establishes a new *containing block*. An absolutely positioned item is taken out of flow, and can then be positioned from the edge of its containing block using the physical offset properties.

Example:

If we want the box to be positioned inside the container, and to have the offsets calculated from the edge of the container, we need to establish a containing block on that container.

```css
.container {
     width: 400px;
     height: 300px;
     position: relative;
}

.box {
     position: absolute;
     top: 10px;
     right: 10px;
     width: 200px;
}
```

#### Fixed positioning

Fixed positioning enables items to assume a fixed place on screen as the document loads, and then stay in that place instead of scrolling with the rest of the page.

A fixed-position box also uses physical offsets, which position it in relation to the viewport. A common reason to use fixed positioning is to keep a menu on screen when scrolling through a long document.

#### Sticky positioning

An item with `position: sticky` acts as if it is static until the document scrolls to a certain point - at which time it acts as if it is fixed.

Example:

```css
.box {
     width: 200px;
     top: 20px;
     position: sticky;
}
```

As we begin to scroll, once the top of the box is 20 px away from the edge of the viewport, the box "sticks", and the rest of the document scrolls while it remains in place.

### Multiple-column layout

```css
.example {
    column-count: 3;
}
```

You can use `column-width` to specify an ideal width for the column.

If you add a `column-width` and a `column-count`, the `column-count` will be treated as a maximum number of columns—even if the screen gets wide enough to accommodate more at your requested width.

```css
.example {
    column-width: 300px;
    column-count: 3;
}
```

### Flexbox

Example:

```css
.cards {
    display: flex;
    flex-wrap: wrap;
}
```

*One-dimensional layout*: We are laying out items in either a row or a column—we can’t control both at once using flexbox.

When flex items wrap onto a new row, the new row becomes its own flex container. The assigning of available space happens across the individual row. Flexbox will NOT try to line the items up with items in rows above or below.

To address the issue above, set `flex-grow` and `flex-shrink` to `0` and `flex-basis` to `auto`.

```css
.cards li {
     width: calc(33.333333333% - 20px);
     flex: 0 0 auto;
}
```