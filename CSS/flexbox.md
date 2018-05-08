# Flexbox

**Flexbox** is most suitable for working with interface elements and smaller components.

## Declare the flexible box model

```css
.flex-container {
	display: flex;
}
```

This creates a block-level flex container; you can use the alternate `inline-flex` value if you prefer an inline-level container.

A *flex item* is any child of the flex container. By default, flex items are laid out in the direction of the document text (e.g., left to right for English). 

To alter the default layout direction, set the `flex-direction` property on the container:

- `row`: default, lays items out in a row.
- `column`: lays items out from top to bottom in a column. 

## Flexbox alignment

In Flexbox, the *main axis* goes in the direction that items are placed, from left to right or top to bottom as set in `flex-direction`.

The *cross axis* is the line that runs perpendicular to the main axis.

## Reserve the content order

Use the `flex-direction` property to set the order in which the flex items are displayed:

- `row-reverse`: reverse the order of flex items horizontailly displayed in rows.
- `column-reverse`: reverse the order of flex items vertically displayed in columns.

## Fully reorder content

Apply the `order` property to flex items. The value of `order` is a number that creates an ordinal group that groups together items with the same value and orders them by their ordinal group from small to big. 

Note:

- Any items without a declared value are shown first because they have the default value of 0.
- Items with the same ordinal group number are grouped in the order in which they appear in the DOM.

## Add flexibility

### `flex-grow`

Use the `flex-grow` property to expand flex items to fill their container.

Example:

```css
.flex-item {
	flex-grow: 1;
}
```

The value of the `flex-grow` property is a ratio that’s used to distribute the empty space between the flex items so they expand. Higher number results in a bigger size.

### `flex-shrink`

Use the `flex-shrink` to shrink flex items to fit within the container.

Example:

```css
.flex-item {
	flex-shrink: 1;
}
```

The value of the `flex-shrink` property is a ratio that’s used to distribute the size reduction among the flex items. Higher numbers reduce the elements by a greater factor.

### `flex-basis`

The width of flex items can be set either by the content they contain or by an explicit `width` value, and any growth or shrinkage is calculated from that base width. To change how the width adjustment is calculated, you can set a `flex-basis` value on an element.

```css
.flex-item {
	flex-basis: 100px;
}
```

When `flex-basis` is applied, any existing width value is ignored, and the value that you specify for the `flex-basis` is used to calculate the adjustment.

### The `flex` shorthand

Example:

```css
#flex-item-a {
	flex: 1 2 150px; /* flex-grow, flex-shrink, flex-basis */
}
```

## Alignment inside the container

### Horizontal alignment with `justify-content`

Syntax:

```css
.flex-container {
	justify-content: keyword;
}
```

The `keyword` can be:

- `flex-start`: default, which aligns all flex items to the left of the parent with the unused space occupying the remaining width to the right.
- `flex-end`, which aligns items to the right of the container with the unused space to the left.
- `center`, which distributes the unused space to either side of all items, centering the items in the container.
- `space-between`, which adds an equal amount of space between each item but none before the first or after the last item.
- `space-around`, which puts an equal amount of space on both sides of each item.

### Vertical alignment with `align-items`

Syntax:

```css
.flex-container {
	align-items: keyword;
}
```

The `keyword` can be:

- `stretch`, which makes items the same height as the parent.
- `flex-start`, which aligns items to the top of the container.
- `flex-end`, which aligns items to the bottom of the container.
- `center`, which aligns items to the vertical center of the container, with equal space above and below.

The default value is `stretch` if the items have no height explicitly specified, or `flex-start` if they do.

### Cross-axis alignment with `align-self`

`align-self` controls the cross-axis alignment of individual items. This property applies to the item, not the container.

Example:

```css
#item {
	align-self: flex-start;
}
```

The values are the same as for `align-items`, and they have the same effects on the selected item only; sibling items are unaffected.

### Wrap and flow

The `flex-wrap` property controls whether items wrap to multiple lines. It can be set to:

- `nowrap`: default, which preserves all items on the same line.
- `wrap`: breaks items onto extra lines below the first (or to the right in column view), if required.
- `wrap-reverse`: changes the direction of the cross axis so new lines appear above (or to the left).

### The `flex-flow` shorthand

Example:

```css
.flex-container {
	flex-flow: column wrap-reverse;
}
```

### Aligning multiple lines with `align-content`

When items wrap over multiple lines, you can control their alignment with the `align-content` property. This property works like `justify-content` but on the cross axis. 

Possible values: `flex-start`, `flex-end`, `center`, `space-between`,`space-around`, `stretch` (resizes the items to fill all unused space).

## An example

You can use Flexbox for displaying the elements in center if the parent component(div) contains “more than one child components/elements(div)” for specific structure. 

```css
div.child {
	display: flex;
	align-items: center; /* cross axis (vertical) alignment */
	justify-content: center; /* main axis (horizontal) alignment */
}
```
