# CSS Grid

## Terminology

- Grid container: The container element that acts as the boundary and sets the dimensions of the grid.
- Grid lines: The dividing lines between rows and columns. These lines are notional, not actual.
- Grid tracks: A shorthand name for both rows and columns. Each column or row created in the grid is referred to as a *track*. Tracks are the spaces between lines.
- Grid cells: Each intersection of a column and a row creates a *cell*. These are like cells in a table.
- Grid areas: A cell or multiple cells that mark the space in which a grid item will be placed.
- Grid items: Each child element placed in the grid.

## Declare and define the grid

For the grid container, use:

```css
div {
    display: grid;
}
```

### Create explicit grids by setting track size

Set `grid-template-columns` and `grid-template-rows` to space-separated list of lengths, which sets the width of the column or the height of the row.

Example:

```css
div {
    grid-template-columns: 60px 3fr 1fr;
    grid-template-rows: 60px auto 5em;
    grid-gap: 20px 30px; /* grid-row-gap grid-column-gap  */
}
```

You can use the specialized grid unit of length, `fr`, or *franction*. One `fr` is equivalent to one equal share of any *unassigned* length in a grid. Grid is only sharing out the available space *after* ensuring that the tracks are big enough to contain the items.

### Place items in an explicit grid

Every immediate child of a grid container becomes a *grid item* and should be placed in the grid by assigning the item a cell coordinate using a set of placement properties:

`grid-column-start`, `grid-row-start`: the line at the start of a grid track (column or row) and the combined track references create the coordinate of a cell.

Example:

```css
/* An item placed on the grid in the second row of the second column */
#c22 {
    grid-column-start: 2;
    grid-row-start: 2; 
}
```

To cover multiple cells, use `grid-column-end` and `grid-row-end`, which designates the line that the cell should end in.

Example:

```css
/* Row 1 to 3 */
#row13 {
    grid-row-start: 1;
    grid-row-end: 4;
}
```

Or you can use the `span` keyword:

```css
#row13 {
    grid-row-end: span 3;
}
```

### Grid placement shorthand properties

```css
#cell {
    grid-column: 2 / 3; 
    /*
        grid-column-start: 2;
        grid-column-end: 3;
    */

    grid-row: 1 / span 3;
    /*
        grid-row-start: 1;
        grid-row-end: span 3;
    */
}
```

Or:

```css
#cell {
    grid-area: row-start / column-start / row-end / column-end;
}
```

### Repeat grid lines

The `repeat()` function takes two arguments: an integer that sets the number of repetitions, followed by a comma separator, and the grid line values to be repeated.

Example:

```css
#container {
    grid-template-columns: 1fr repeat(11, 10px 1fr);
    /*
        12 columns of 1fr each, 10px gutter
    */
}
```

### Named grid areas

Use the `grid-template-areas` property. 

Example 1:

```css
#container {
    display: grid;
    grid-template-areas: `nav main side`;
    grid-template-columns: repeat(3, 1fr);
}

#itemMain {
    grid-area: main;
}
```

Example 2:

```css
#container {
    display: grid;
    grid-template-areas:
      'nav head head'
      'nav main side';
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: 80px auto;
}

#F { grid-area: head; }
#G { grid-area: nav; }
```

### The `grid-template` shorthand

Syntax:

```css
#container {
    grid-template: grid-template-columns / grid-template-rows;
}
```

To use the property with named grid areas, you add the identifiers after the slash:

```css
#container {
   grid-template: repeat(3, 1fr) / 'nav head head' 80px 'nav main side' auto; 
}
```

### Implicit grids

Implicit grids are defined by their contents, rather than the specified length values of explicit grids.

`grid-auto-columns` and `grid-auto-rows`: take a single value to specify the width of the row or column.

Example:

```css
#container {
    display: grid;
    grid-auto-columns: 1fr;
    grid-auto-rows: 80px;
    /*
        Any created columns should be 1fr wide
        any new rows should be 80px
    */
}
```

### Grid items without a decleared place

```css
#container {
    grid-auto-flow: keyword;
}
```

The `keyword` can be:

- `column`: Items will fill empty cells in columns, moving down the column.
- `row`: Items will fill empty rows, moving across the row.

## Combine explicit and implicit grids

The following code creates an explicit grid of three columns and two rows and allows for any items exceeding this explicit grid by adding an implicit grid. The extra columns in the implicit grid are defined as 1fr wide, with extra rows being 80px high:

```css
#container {
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 80px);
    grid-auto-columns: 1fr;
    grid-auto-rows: 80px;
}
```

### The `grid` shorthand

Syntax: 

```css
#container {
    grid: grid-auto-flow grid-auto-columns / grid-auto-rows;
}
```

Note you can only use `grid` to set either explicit or implicit grids, not both.

Example:

```css
/* Implicit grid */
#container {
    grid: row 1fr / 80px;
}

/* Explicit grid */
#container2 {
    grid: repeat(3, 1fr) / 'a b b' 80px 'a c d' auto;
}
```

## Grid item stacking order

Use the `z-index` property: items with the highest `z-index` value will be stacked above all others.

Use the `order` property: In explicit grids, this property acts exactly like `z-index`, changing the stacking order; in implicit grids, however, it also changes the order in which items are placed in the grid.

## The `minmax()` function

The `minmax(min, max)` CSS function defines a size range greater than or equal to `min` and less than or equal to `max`.