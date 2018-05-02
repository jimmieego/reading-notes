## Text shadow

Syntax:

```css
h2 {
	text-shadow: 3px 3px 3px #BBB; /* x-offset, y-offset, blur radius, color */
}
```

You can add multiple shadows by separating them using commas (`,`).

## Restricting overflow

Text is clipped at the point where it flows out of the container element:

```css
p {
	text-overflow: clip;
}
```


Replaces the last whole or partial character before the overflow with an ellipsis character (`...`):

```css
span {
	text-overflow: ellipsis;
}

```