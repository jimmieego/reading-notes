# New CSS Features

## Custom Properties (Variables)

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

Using fallback values: pass in the default value as the second argument of the `var()` function:

```css
.button {
    background-color: var(--button-background-color, gray);
}

.button-primary {
    background-color: var(--primary-button-background-color, var(--button-background-color, gray));
}
```

Custom properties can be redefined within media queries. Instead of redefining the spacing properties on the element, just redefine the custom properties within the media queries. Example:

```css
:root {
    --card-padding: 1rem;
}

@media (min-width: 600px) {
    :root {
        --card-padding: 1.25rem;
    }
}

@media (min-width: 1000px) {
    :root {
        --card-padding: 1.5rem;
    }
}

.card {
    padding: var(--card-padding);
}
```

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