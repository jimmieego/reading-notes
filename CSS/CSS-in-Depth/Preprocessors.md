# Preprocessors

## Sass

### Install Sass

1. Create a new project directory and navigate to it in terminal.
2. Run `npm init -y`: initializes a new npm project, creating a `package.json` file.
3. Run `npm install --save-dev node-sass`: installs the `node-sass` package and adds it to package.json as a development dependency.

### Run Sass

In the project directory, create two subdirectories: `sass` and `build`.

You’ll put your source files in the sass directory, and Sass will use those files to produce a CSS file in the build directory.

Edit the `package.json` file and change the `scripts` entry to:

```
"scripts": {
  "sass": "sass sass/index.scss build/styles.css"
},
```

Run `npm run sass` execute the command above and produce/overwrite the stylesheet at `build/styles.css`.

### Sass features

#### Inline computation

Sass supports inline arithmetic using `+`, `-`, `*`, `/`, and `%` (for modular division). This feature is useful when two values are related, but not the same.

#### Nested selectors

Sass allows you to nest selectors inside other declaration blocks. You can use nesting to group related code in the same block.

Example:

```css
site-nav {
  display: flex;

  > li {
    margin-top: 0;
    
    /* Ampersand indicates where the outer selector will be appended. */
    &.is-active {
      font-weight: bold;
    }
  }
}
```

By default, the outer `.site-nav` selector is prepended to every selector in the compiled code, and a space is added where the selectors are joined. To change this, use an ampersand (`&`) to indicate where you want the outer selector to be inserted.

Note: Nesting increases the specificity of the resulting selectors. Be cautious about nesting and avoid nesting several levels deep.

Nest a media query:

```css
html {
  font-size: 1rem;
  @media (min-width: 45em) {
    font-size: 1.25rem;
  }
}
```

This way, if you change a selector, you won’t have to remember to change the corresponding selector in a media query to match.

#### Partials (`@import`)

Partials let you split your styles into multiple separate files, and Sass will concatenate them all together into one file.

#### Mixins

A *mixin* is a small chunk of CSS that you can re-use throughout your stylesheet.

Example:

```css
@mixin clearfix {
  &::before {
    display: table;
    content: " ";
  }
  &::after {
    clear: both;
  }
}

.media {
  @include clearfix;
  background-color: #eee;
}
```

Example with parameters:

```css
@mixin alert-variant($color, $bg-color) {
  padding: 0.3em 0.5em;
  border: 1px solid $color;
  color: $color;
  background-color: $bg-color;
}

.alert-info {
  @include alert-variant(blue, lightblue)
}

.alert-danger {
  @include alert-variant(red, pink)
}
```

#### Extend

In general, you should probably favor mixins. Only use `@extend` when you want to shorten the number of class names needed in your HTML.

Example:

```css
.message {
  padding: 0.3em 0.5em;
  border-radius: 0.5em;
}
.message-info {
  @extend .message;
  color: blue;
  background-color: lightblue;
}
.message-danger {
  @extend .message;
  color: red;
  background-color: pink;
}
```

This compiles to:

```css
.message,
.message-info,
.message-danger {
  padding: 0.3em 0.5em;
  border-radius: 0.5em;
}
.message-info {
  color: blue;
  background-color: lightblue;
}
.message-danger {
  color: red;
  background-color: pink;
}
```

#### Color manipulation

By using functions, you can edit the value of one variable, but allow the change to affect other, related, colors.

Example:

```css
$green: #63a35c;

$green-dark: darken($green, 10%);
$green-light: lighten($green, 10%);

$green-vivid: saturate($green, 20%);
$green-dull: desaturate($green, 20%);

$purple: adjust-hue($green, 180deg);
$yellow: adjust-hue($green, -70deg);

$green-transparent: rgba($green, 0.5);
```

#### Loops

Example:

```css
@for $index from 2 to 5 {
   .nav-links > li:nth-child(#{$index}) {
    transition-delay: (0.1s * $index) – 0.1s;
  } 
}
```