# CSS in Depth

Keith J. Grant

## 1. Cascade, specificity, and inheritance

### Cascade

When declarations conflict, the cascade considers three things to resolve the difference:

1. *Stylesheet origin* — Where the styles come from. Your styles are applied in conjunction with the browser’s default styles.
2. *Selector specificity* — Which selectors take precedence over which.
3. *Source order* — Order in which styles are declared in the stylesheet.

![High-level flowchart of the cascade showing declaration precedence](images/cascade-flowchart.png)

#### Stylesheet origin

1. Author important (`!important` added to the end of declaration)
2. Author
3. User agent

#### Specificity

- Inline styles have no selector because they are applied directly to the element they target. To override inline declarations in your stylesheet, you’ll need to add an `!important` to the declaration, shifting it into a higher-priority origin. If the inline styles are marked important, then nothing can override them. It’s preferable to do this from within the stylesheet.
- Selector specificity (ID > Class > Tag):
  - If a selector has more IDs, it wins.
  - If that results in a tie, the selector with the most classes wins. 
  - If that results in a tie, the selector with the most tag names wins.

Notes:

- Pseudo-class selectors (for example, `:hover`) and attribute selectors (for example, `[type="input"]`) each have the same specificity as a class selector. The universal selector (`*`) and combinators (`>`, `+`, `~`) have no effect on specificity.
- If you need to override a style applied using an ID, you have to use another ID.
- It is generally best to keep specificity low when you can, so when you need to override something, your options are open.

#### Source order

If the origin and the specificity are the same, then the declaration that appears later in the stylesheet—or appears in a stylesheet included later on the page—takes precedence.

### Two rules of thumb

1. Don't use IDs in your selector.
2. Don't use `!important`.

Include a stylesheet for your component. If your component needs to make style changes dynamically, it's almost always preferable to use JavaScript to add and remove classes to the elements.

### Inheritance

If an element has no cascaded value for a given property, it may inherit one from an ancestor element.

Primarily properties pertaining to text, list properties, and table border properties are inherited.

In browser's dev tools, the style inspector shows every selector targeting the inspected element, ordered by specificity. Styles closer to the top override those below. Overridden styles are crossed out.

`inherit`: You can override another value with this, and it will cause the element to inherit that value from its parent.

`initial`: If you assign the value `initial` to a property, then it effectively resets to its default value.

Examples:

- `border: initial`: Remove a border from an element.
- `width: initial`: Restore an element to its default width. Or use `width: auto`, because the default value of `width` is `auto`.

### Shorthand properties

Most shorthand properties let you omit certain values and only specify the bits you’re concerned with. Note that doing this still sets the omitted values to their initial value.

**Top, Right, Bottom, Left**: The order of properties that apply individually to all four sides of the box like a clock (e.g., `margin` and `padding`). If the declaration ends before one of the four sides is given a value, that side takes its value from the opposite side. If you specify only one value, it will apply to all four sides.

**Horizontal, Vertical**: The order of properties that only support up to two values (e.g., `background-position`). The two values represent a Cartesian grid.

## Working with relative units

When you’ve multiple ways to solve a particular problem, you’ll need to favor the solution that works more generally under multiple and different circumstances.

### em

`em`: 1 em means the font size of the current element.

Using ems can be convenient when setting properties like `padding`, `height`, `width`, or `border-radius` because these will scale evenly with the element if it inherits different font sizes, or if the user changes the font settings.

`font-size` ems are derived from the *inherited* font size. For most browsers, the default font size is 16px.

### rem

`rem`: relative to the root element.

The `:root` pseudo-class selector is equivalent to the `html` type selector.

Use rems for font sizes, pixels for borders, and ems for most other measures, especially paddings, margins, and border radius. Use percentages for container widths when necessary.

### Setting default font size

```css
:root {
    font-size: 0.875em; /* 14 px; 14/16 = 0.875 */
}
```

### Viewport-relative units

Viewport-relative units define lengths relative to the browser's viewport.

- `vh`: 1/100th of the viewport height
- `vw`: 1/100th of the viewport width
- `vmin`: 1/100th of the smaller dimension, height or width
- `vmax`: 1/100th of the larger dimension, height or width

Using `calc()` for font size;

```css
:root {
    font-size: calc(0.5em + 1vw);
}
```

This will make the font scale smoothly.

### Unitless numbers

Properties that allow for unitless values:

- `line-height`: this can prevent the overlapping text because of small line height.
- `z-index`
- `font-weight`: `700` is equivalent to bold; `400` is equivalent to normal

Example:

```css
body {
    line-height: 1.2; /* Descendant elements inherit the unitless value */
}
```

When you use a unitless number, that declared value is inherited, meaning its com- puted value is recalculated for each inheriting child element.

### Custom properties (CSS variables)

The name must begin with two hypthens (`--`). Variables must be declared inside a declaration block.

Example:

```css
:root {
    --main-font: Helvetica, Arial, sans-serif;
    --brand-color: #369;
}

p {
    font-family: var(--main-font, sans-serif);
    color: blue; /* fallback */
    color: var(--brand-color, blue); /* blue is the fallback value */
}
```

The `var()` function accepts a second parameter, which specifies a fallback value.

The declarations of custom properties cascade and inherit: You can define the same variable inside multiple selectors, and the variable will have a different value for various parts of the page. The custom properties behave as a sort of scoped variable because the values are inherited by descendant elements.

Use JavaScript to access custom properties:

```javascript
var rootElement = document.documentElement;
var styles = getComputedStyle(rootElement);
var mainColor = styles.getPropertyValue('--main-bg');

rootElement.style.setProperty('--main-bg', '#cdf');
```