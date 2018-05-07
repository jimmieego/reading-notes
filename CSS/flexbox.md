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




You can use Flexbox for displaying the elements in center if the parent component(div) contains “more than one child components/elements(div)” for specific structure. 

```css
div.child {
	display: flex;
	align-items: center; /* vertical alignment */
	justify-content: center; /* horizontal alignment */
}
```
