## Shadow DOM

The CSS inside shadow DOM trees only applies inside that element. 

## Inline children

```css
/* parent */
div.parent {
	display: inline;
}

div.child {
	display: inline-block; /* place children inline/horitonzally inside parent */
}
```

## Flexbox
Flexbox is best way for displaying the elements in center if the parent component(div) contains “more than one child components/elements(div)” for specific structure.

```css
div.child {
	display: flex;
	align-items: center;
	justify-content: center;
}
```
