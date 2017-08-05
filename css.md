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
h2 ~ p { }

## Attribute selectors
- Select an attribute name: `input[type="text"]`
- Select from a list of values: `*[class~=box]` selects any element with a class of `box`.
- Select a value that starts with a string: `a[href^="https"]`
- Select a value that ends with a string: `a[href$=".com"]`
- Select a value that contains a string: `a[href*=".com"]`
- Case insensitivity: `a[href^="http" i]`
- Select a value or a value followed by a `-`: `span[lang|="en"]`

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
A mixin is a collection of of re-usable styles, properties and selectors.

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
