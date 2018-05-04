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
	column-width: 150px; /* 150px here is the minimum column width */
}
```

## Varying distribution of content across columns

```css
div {
	column-fill: balance; /* balance is default; can also set to `auto`, which fills columns sequentially when the parent element has a fixed height. */
}
```

You can set both `column-count` and `column-width`: the `column-count` value acts as a maximum and the `column-width` acts as a minimum. A shorthand syntax:

```css
div {
	columns: 150px 3; /* column-width, column-count */
}
```

## Column gaps and rules

`column-gap`: sets the space between columns.

`column-rule`: draws a line equidistantly between columns.

```css
div {
	column-rule: 0.3em double silver; /* column-rule-width, column-rule-style, column-rule-color */
}
```

## Elements spanning multiple columns

```css
div h2 {
	column-span: all; 
}
```

The default of `column-span` is `none`. 

Setting `column-span` to `all` provides a break in the flow — all content before the element will be distributed into columns, and all content after the element will be distributed into columns, but the element itself — known as the *spanning element* — will not.