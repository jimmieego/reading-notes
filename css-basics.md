<!-- MarkdownTOC -->

- Selectors
	- Child selector
	- Adjacent sibling
	- General sibling
	- Attribute selectors
	- Pseudo-class selectors
	- Pseudo-element selectors
- Units
	- Absolute units
	- Relative units
	- Viewport percentage units

<!-- /MarkdownTOC -->


# Selectors
## Child selector
Select all elements that are immediate children of a specified parent. 

```css
.classname > a { }
```

## Adjacent sibling
Select elements that are the adjacent siblings of an element.

```css
h2 + p { }
```

## General sibling
Select elements that are the siblings of an element.

```css
h2 ~ p { }
```

## Attribute selectors
- Select an attribute name: `input[type="text"]`
- Select from a list of values: `*[class~=box]` selects any element with a class of `box`.
- Select a value that starts with a string: `a[href^="https"]`
- Select a value that ends with a string: `a[href$=".com"]`
- Select a value that contains a string: `a[href*=".com"]`
- Case insensitivity: `a[href^="http" i]`
- Select a value or a value followed by a `-`: `span[lang|="en"]`

## Pseudo-class selectors
- `:first-child`: target an element when it is the first child of a parent.
- `:last-child`: target an element when it is the last child of a parent. 
- `:nth-child`: select multiple elements according to their position in the document tree. 
	- `:nth-child(2)`: 2nd child
	- `:nth-child(odd)` or `:nth-child(2n+1)`: odd children
	- `:nth-child(even)`: even children
- `:nth-of-type`: select multiple elements according to their position in the document tree but only those elements that are the same as the type the rule is applied to. Example: `p:nth-of-type(odd){ }`
- `:only-child`: match if the element is the only child of the parent.
- `:empty`: match if an element is completely empty or just contains an HTML comment.
- `:not`: allows you do something if a selector does not match. Example: `td:not(.animal) { }`

## Pseudo-element selectors
- `::first-letter`: the first character of the first line of text.
- `::first-line`: the first formatted line of text.
- `::before` and `::after`: give us the ability to insert generated content before and after another element. Example: `.classname::before {content:"Content inserted before";}`

# Units
## Absolute units
`px`: You should avoid using absolute units when your aim is to create a flexible and responsive site. However absolute units can be useful in components when you know you do not want the area to stretch. They can also be helpful in defining `max-width` and `min-width`to stop areas becoming too narrow or too wide.

## Relative units
- `em`: Using `em` as a length unit in layout, and in particular in padding and margins can help to maintain a vertical rhythm.
- `rem`: The `rem` (root `em`) unit is the font-size of the root element, which is usually the `html` element.

## Viewport percentage units
- `vh`: 1/100th of the height of the viewport. `100vh` is the full height of the viewport.
- `vw`: 1/100th of the width of the viewport.
- `vmin`: equal to the smaller of `vh` or `vw`.
- `vmax`: equal to the larger of `vh` or `vw`.