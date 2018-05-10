New CSS Features

## Variables

Define a *custom property*:

1. Set its scope;
2. Create a unique identifier;
3. Assign the identifier a value.

Example:

```css
/* global scope */
:root {
	--fooColor: #f00;
}

E {
	border-color: var(--fooColor);
}

/* limited scope */
h1 {
	--fooColor: #f00;
}

h1 {
	color: var(--fooColor);
}
```

CSS variable names must be a string of characters with no spaces and prefixed with a double hyphen to avoid conflict with other defined values. Any valid CSS property value is permitted.

## Feature queries

Example:

```css
@supports (display: flex) { ... }
@supports (display: flex) and (transition: 1s) {...}
@supports not (display: flex) {...}
```

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