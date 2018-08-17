# The New CSS Layout

Rachel Andrew

## 2. Where we are

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

## 3. The new layout

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

### CSS Grid

Example:

```css
.cards {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;
    gap: 20px; /* new name */
}

.card1 {
    grid-column: 1 / 3;
    grid-row: 1;
}

.card2 {
     grid-column: 3;
     grid-row: 1;
}

.card3 {
     grid-column: 1;
     grid-row: 2 / 4;
}

.card4 {
     grid-column: 2 / 4;
     grid-row: 2;
}

.card5 {
     grid-column: 2 / 4;
     grid-row: 3;
   }
```

Use *named areas*:

```css
.card1 { grid-area: a; }
.card2 { grid-area: b; }
.card3 { grid-area: c; }
.card4 { grid-area: d; }
.card5 { grid-area: e; }

.cards {
     display: grid;
     grid-template-columns: 1fr 1fr 1fr;
     grid-gap: 20px;
     grid-template-areas:
       "a a b"
       "c d d"
       "c e e";
}
```

To leave white space, and to leave a cell empty, use a full-stop character such as `.`.

## 4. Alignment control

### Aligning flex items

Set `align-items` to the flex container:

- `flex-start`: align items at the top of the container.
- `flex-end`: send items all to the bottom.
- `center`: center all items.

Set `align-self` on an individual flex item to override the `align-items` setting.

Alignment works on items on the *cross axis* (*column axis* in the Grid specification). Flex items are displayed as a row; the cross axis runs across the row vertically, stretching the height of the flex container.

If we change the `flex-direction` to `column`, the cross axis becomes horizontal. Aligning the items to `flex-end` moves the column over to the right-hand side.

The `justify-content` property affects the entire flex container. The `justify-content` property acts on the **main axis**—on the row if our `flex-direction` is `row`, on the column if `flex-direction` is `column`. The initial value of `justify-content` is `flex-start`.

The `justify-content` property is also the property used to space items out along the main axis:

- `space-between`: creates an equal amount of space between items.
- `space-around`: creates an equal amount of space around the items.
- `space-evenly`: distributes the items evenly on the main axis.

The `align-content` property works on the **cross axis** in flexbox, which will only have free space available if the following conditions are met:

- `flex-wrap` is `wrap`
- The container is taller than the space needed to display the items

If both of these things are true, you can use `align-content` in the same way as justify content.

### Aligning grid items

The `align-items` and `align-self` properties still apply. The default value for `align-items` is `stretch`.

Set the alignment of grid items along the row (or inline) axis with the `justify-items` property, which sets the `justify-self` value of the individual grid items. The initial value of `justify-items` in Grid Layout is `stretch`, so the items stretch over their entire area.

### Aligning and justifying grid tracks

The `align-content` and `justify-content` properties affect the grid tracks in Grid Layout. 

### The simplest way to center a box

```css
.example {
     height: 50vh;
     display: flex;
     justify-content: center;
      align-items: center;
}
```

As with `align-content` in flexbox, you need additional space in the grid container for these to work (e.g., using fixed-sized tracks).

### Alignment with auto margins

Example:

```css
.cards {
     display: flex;
}

.cards li:last-child {
     margin-left: auto;
}
```

The margin of the last card takes up all the space and pushes that one item over to the right.

## 5. Responsive by default

Use `auto-fill` with a fixed-size value:

```css
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, 200px);
}
```

Note:

- If we used `1fr`, we would only get one column track, since `1fr` would use all the available space in the grid container.
- `minmax()` sets a minimum and maximum size for a track.
- Use `auto-fill` if you want to maintain the tracks; use `auto-fit` if you want the content to fill the container in case there are fewer items than tracks.

### Flexible sizing in flexbox

In flexbox, the key to flexible sizing lies in three properties: `flex-grow`, `flex-shrink`, and `flex-basis`. These are applied to the flex items.

The `flex-basis` can be used to set a width on the main axis for the flex item. It can accept a length unit, or the keywords `content` and `auto`.

- `flex-basis: content;`: the `flex-basis` is taken from the content size of the item in the main axis.
- `flex-basis: auto;`: if you’ve set a width on the item, that width will be used as the `flex-basis` value. If you haven’t set a width, auto resolves to the content size.

The `flex-grow` defines whether an item can grow larger than the size set in `flex-basis`.

The `flex-shrink` determines whether an item can shrink smaller than the `flex-basis` value.

The `flex` shorthand: order of the values is: `flex-grow` `flex-shrink` `flex-basis`.

### Sizing in grid

In Grid: The `fr` unit is used when creating track sizes.

Using `auto` as a maximum in `minmax()`: This enables the creation of tracks that are always a minimum height or width, but that expand if more content is added than expected.

## 6. Source order and display order

