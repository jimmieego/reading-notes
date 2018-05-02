<!-- MarkdownTOC -->

- Selectors
	- DOM selectors
		- Attribute selectors
	- Pseudo-selectors
		- Child selector
		- Adjacent sibling
		- General sibling
		- Pseudo-class selectors
			- For selecting child
			- For selecting type
			- Others
		- Pseudo-element selectors
		- UI element states
		- Constraint Validation Pseudo-classes
- Units
	- Absolute units
	- Relative units
	- Viewport percentage units

<!-- /MarkdownTOC -->


# Selectors

Selectors can be separated into two categories: DOM selectors (class, type, attribute) and Pseudo-selectors.

## DOM selectors

### Attribute selectors

```
E[attr] {...} /* Simple Attribute Selector */
E[attr='value'] {...} /* Exact Attribute Value Selector */ 
E[attr~='value'] {...} /* Partial Attribute Value Selector, matches a full item in a space-separated list */ 
E[attr|='value'] {...} /* Language Attribute Selector */
```

Select an attribute name: `input[type="text"]`

Select from a list of values: `*[class~=box]` selects any element with a class of `box`.

Select a value that starts with a string: `a[href^="https"]`. Example of showing an icon for external links:
  
```css
  a[href^='http'] {
    background: url('link.svg') no-repeat left center;
    display: inline-block;
    padding-left: 20px;
  }
```

Select a value that ends with a string: `a[href$=".com"]`. Example:

```css
a[href$='.pdf'] { background-image: url('pdf.svg'); }
a[href$='.doc'] { background-image: url('word.svg'); }
a[href$='.rss'] { background-image: url('feed.svg'); }
```

Select a value that contains a string or a *substring*: `a[href*=".com"]`

Case insensitivity: `a[href^="http" i]`

Select a value or a value followed by a `-`: `span[lang|="en"]`

You can chain multiple selectors together:

```css
a[href^='http://'][href*='/folder2/'][href$='.pdf'] {...}
```

## Pseudo-selectors

### Child selector

Select all elements that are *immediate* children of a specified parent. 

```css
.classname > a { }
```

### Adjacent sibling

Select elements that are the *immediate*, *adjacent* siblings of the first selector.

```css
h2 + p { }
```

### General sibling

Select any elements that are preceded by the first selector, regardless of whether it is immediately adjacent.

```css
h2 ~ p { }
```

### Pseudo-class selectors

#### For selecting child

- `:first-child`: target an element when it is the first child of a parent.
- `:last-child`: target an element when it is the last child of a parent. 
- `:nth-child`: select multiple elements according to their position in the document tree. For `:nth-child(n)`, `n` represents a number that begins at `0` and increments by `1`.
 - `:nth-child(2)`: 2nd child
 - `:nth-child(odd)` or `:nth-child(2n+1)`: odd children
 - `:nth-child(even)` or `:nth-child(2n)`: even children
- `:nth-last-child()`: accepts the same arguments as `:nth-child()`, except counted from the last element, working in reverse. For example: `tbody tr:nth-last-child(-n+2) { font-style: italic; }`. Note the use of `-n` to increase the count negatively.
- `:only-child`: match if the element is the only child of the parent.

#### For selecting type

- `:nth-of-type`: select multiple elements according to their position in the document tree but only those elements that are the same as the type the rule is applied to. Example: `p:nth-of-type(odd){ }`
- `:nth-last-of-type`: accepts the same arguments as `:nth-of-type()`, except counted from the last element, working in reverse.
- `:first-of-type`: select the element that is the first child of the named type of its parent.
- `:last-of-type`
- `:only-of-type`: select elements in the document tree that have a parent but no siblings of the same type.
- `:empty`: match if an element is completely empty or just contains an HTML comment.
- `:not`: allows you do something if a selector does not match. Example: `td:not(.animal) { }`

Note: 
- Where every child is of the same type, `:nth-child()` and `:nth-of-type()` are interchangeable.
- Using `:only-of-type` allows you to pick an element from among others, whereas `:only-child` requires the element to sit alone.

#### Others

A pseudo-class differentiates among an element’s different states or types; these include—but are not limited to—those that provide information about link states: `:hover`, `:visited`, `:active`, and so on.

`:target`: allows you to appl styles to the element when the referring URI has been followed.

`:empty`: selects an element that has no children, including text nodes.

`:root`: selects the first element in a DOM tree. In HTML, the root will always be the `html` element.

`:not()`: selects all elements *except* those that are given as the value of an argument. This example colors all the immediate child elements of a `div`, except for `p` elements:

```css
div > :not(p) {
	color: red;
}
```

Note: The argument passed into `:not()` must be a simple selector. Combinators such as `+` and `>` and pseudo-elements are not valid values. 

### Pseudo-element selectors

A pseudo-element provides access to an element’s subpart, which includes those pseudo-elements that select portions of text nodes; for instance, `:first-line` and `:first-letter`. Note that the pseudo-elements are prefixed with a double colon (::).

- `::first-letter`: the first character of the first line of text.
- `::first-line`: the first formatted line of text.
- `::before` and `::after`: give us the ability to insert generated content before and after another element. Example: `.classname::before {content:"Content inserted before";}`

### UI element states

```
:checked {...}
:disabled {...}
:enabled {...}
```

Example:

```css
input[type='text']:disabled { border: 1px dotted gray; }
input[type='text']:enabled { border: 1px solid black; }
```

### Constraint Validation Pseudo-classes

We can style elements depending on whether they’re required or optional by using their namesake pseudo-classes:

```
:required {...}
:optional {...}
```

Each form field can be in one of two states of validation: either valid or invalid. The pseudo-classes:

```
:valid {...}
:invalid {...}
```

Some HTML5 elements can have a permitted range of values, set by using the `min` and `max` attributes. You can style these elements depending on whether the current value is in or out of range by using:

```
:in-range {...}
:out-of-range {...}
```

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