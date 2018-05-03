## Prescriptive columns

Use the `column-count` property:

```css
p.columns-2 {
	column-count: 2;
}
```

## Dynamic columns

You use the `column-width` property to specify the width of each column, and the browser fills the parent element with as many columns as can fit along its width.

```css
div {
	column-width: 150px; /* 150px here is the minimum column width*/
}
``` 