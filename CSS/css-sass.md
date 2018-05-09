# Sass

Never edit or commit .css files.

## Variables

Example:

```css
$site_max_width: 960px;
$font_color: $333;
$link_color: $00c;
$font_family: Arial, sans-serif;
$font_size: 16px;
$line_height: percentage(20px / $font_size);

body {
  color: $font_color;
  font {
    size: $font_size;
    family: $font_family;
  }
  line-height: $line_height;
}

#main {
  width: 100%;
  max-width: $site_max_width;
}
```

## Functions and Operators

## Mixins

A *mixin* is a collection of of re-usable styles, properties and selectors.

Examples:

```css
@mixin box-shadow($shadow) {
  -webkit-box-shadow: $shadow;
     -moz-box-shadow: $shadow;
          box-shadow: $shadow;
}

@mixin hide-text {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
```

Use something like `@import "global/mixins;"` to include component `.scss` files. Make sure use an underscore (`_`) character at the start of the file name (e.g., `_variables.scss`). The Sass compiler will interpret these files as snippets and won’t actually preprocess them individually. Only the files you want the preprocessor to compile should be named without an underscore, e.g., `style.scss`.

## Compass

Minimum `config.rb` file in the root of project folder:

```
http_path = "/"
css_dir = "css"
sass_dir = .scss"
images_dir = "images"
javascripts_dir = "js"
fonts_dir = "fonts"

output_style = :expanded
environment = :development
```

Import Compass:

```
@import "compass";

@import "global/mixins";
```

Or:

```
@import "compass/utilities";
@import "compass/css3";
@import "compass/typography/vertical_rhythm";

@import "global/mixins";
```

# Flexbox

Reference: https://css-tricks.com/snippets/css/a-guide-to-flexbox/

## Basic concepts

The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate to all kind of display devices and screen sizes). A flex container expands items to fill available free space, or shrinks them to prevent overflow. 

The flexbox layout is direction-agnostic. 

**Note**: Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.

**Flex container**: parent element
**Flex items**: children

Any `:before` and `:after` pseudo-elements on flex container will be treated as children. 

## Flex container (parent) properties

```css
.container {
	display: flex; /* or inline-flex */
	flex-direction: row | row-reverse | column | column-reverse;
	flex-wrap: nowrap | wrap | wrap-reverse;
	flex-flow: <‘flex-direction’> || <‘flex-wrap’>; 
	justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly; /* on main axis */
	align-items: flex-start | flex-end | center | baseline | stretch; /*defines the default behaviour for how flex items are laid out along the cross axis on the current line */
	align-content: flex-start | flex-end | center | space-between | space-around | stretch; /*aligns a flex container's lines within when there is extra space in the cross-axis; this property has no effect when there is only one line of flex items. */
}
```

Note: When switching to `flex-direction: column;`, `align-items` becomes the horizontal alignment while `justify-content` becomes the vertical alignment.

## Flex items (children) properties

```css
.item {
	order: <integer>; /*controls the order in which flex items appear in the flex container */
	flex-grow: <number>; /* default 0; accepts a unitless value that serves as a proportion. */
	flex-shrink: <number>; /* default 1; defines the ability for a flex item to shrink if necessary. */
	flex-basis: <length> | auto; /* default auto; defines the default size of an element before the remaining space is distributed.  */
	flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ] /*This is the shorthand for flex-grow, flex-shrink and flex-basis combined. The second and third parameters (flex-shrink and flex-basis) are optional. Default is 0 1 auto. It is recommended that you use this shorthand property rather than set the individual properties. The short hand sets the other values intelligently.*/
	align-self: auto | flex-start | flex-end | center | baseline | stretch; /* This allows the default alignment (or the one specified by align-items) to be overridden for individual flex items. Note that float, clear and vertical-align have no effect on a flex item. */
}
```