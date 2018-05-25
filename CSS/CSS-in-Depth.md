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

## Mastering the box model

When you set the width or height of an element, you’re specifying the width or height of its *content*; any padding, border, and margins are then added to that width.

![The default box model](images/default-box-model.png)

By default, `box-sizing` is set to the value of `content-box`. This means that any height or width you specify only sets the size of the content box.

You can set `box-sizing` to `border-box`, then the `height` and `width` properties set the combined size of the content, padding, and border. With this model, padding doesn’t make an element wider; it makes the inner content narrower. It also does the same for height.

![The box model with box sizing set to border-box](images/border-box-sizing-model.png)

Apply border box sizing to all elements and pseudo-elements on the page:

```css
/* Adding this snippet near the beginning of your stylesheet */
:root {
    box-sizing: border-box;
}

*,
::before,
::after {
    box-sizing: inherit;
}
```

### Element height

Typically it’s best to avoid setting explicit heights on elements. The height of a container is organically determined by its contents, not by the container itself. When you explicitly set an element’s height, you run the risk of its contents overflowing the container.

`overflow` controls the behavior of overflowing content:

- `visible`: default value; all content is visible, even when it overflows the container’s edges.
- `hidden`: content that overflows the container’s padding edge is clipped and won’t be visible.
- `scroll`: scrollbars are added to the container so the user can scroll to see the remaining content.
- `auto`: scrollbars are added to the container only if the contents overflow.

You can use `overflow-x` or `overflow-y` to control only horizontal or vertical overflow. Explicitly setting both `overflow-x` and `overflow-y` to different values, however, tends to have unpredictable results.

Specifying height using a percentage is problematic. A better approach is to use the viewport-relative `vh` units.

#### Columns of equal height

By default, using a flexbox produces elements of equal height. By applying `display: flex` to the container, it becomes a *flex container*. Its child elements will become the same height by default.

`min-height` and `max-height`: you specify a minimum or maximum value, allowing the element to size naturally within those bounds.

Similar properties `min-width` and `max-width` constrain an element’s width.

#### Vertically centering content

A `vertical-align` declaration only affects inline and table-cell elements. With inline elements, it controls alignment among other elements on the same line. You can use it to control how an inline image aligns with the neighboring text, for example. With table-cell elements, `vertical-align` controls the alignment of the contents within the cell.

Options:

- Can you use a natural height container? Apply an equal top and bottom padding to the container to center its contents.
- Do you need a specific height container, or do you need to avoid using padding? Use `display: table-cell` and `vertical-align: middle` on your container.
- Can you use flexbox? Use `align-items:center`.
- Is the inner content only one line of text? Set a tall line height equal to the desired container height. This will force the container to grow to contain the line height. If the contents aren’t inline, you may have to set them to `inline-block`.

Reference: http://howtocenterincss.com

#### Negative margins

![Behavior of negative margins](images/negative-margins.png)

#### Collapsed margins

*Collapsing*: When top and/or bottom margins are adjoining, they overlap, combining to form a single margin. The size of the collapsed margin is equal to the *largest* of the joined margins.

Example: Paragraphs (`<p>`), by default, have a 1 em top margin and a 1 em bottom margin. When you stack two paragraphs, one after the other, their margins don’t add up to a gap of 2 em. Instead they collapse, overlapping to produce only 1 em of space between the two paragraphs.

This behavior typically means you can style margins on various elements without much concern for what might appear above or below them. The collapsed margin between the elements only appears larger if the following element requires more space.

Note: Margin collapsing only occurs with top and bottom margins. Left and right margins don’t collapse.
