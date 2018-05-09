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
}
```

You can use the specialized grid unit of length, `fr`, or *franction*. One `fr` is equivalent to one equal share of any *unassigned* length in a grid.

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

