Transitions only take effect when the property they are applied to changes value. Animations are explicitly executed when applied to an element.

## Transitions

A *transition* is an *implicit* animation that moves a property between two states. For a transition to occur, four conditions must be in place: an initial value, an end value, the transition itself, and a trigger. All transitions act in reverse when the trigger is no longer active.

Example:

```css
div {
    background-color: black;
    transition: background-color 2s;
}

div:hover { 
	background-color: silver; 
}
```

## `transition-property`

Syntax: `transition-property: keyword;`

`keyword` is `all`, `none`, or a valid CSS property. The default value is `all`, which means every valid property will be animated.

## `transition-duration`

Syntax: `transition-duration: time`. 

`time` is a number of unit of `ms` or `s`.

## `transition-timing-function`

This property has three different value types: a keyword, the `cubic-bezier()` function, or the `steps()` function.

### Timing function keywords

Syntax: `transition-timing-function: keyword;`

The `keyword` can be: `ease`, `linear`, `ease-in`, `ease-out`, and `ease-in-out`. The default value is `ease`.

### The cubic bezier curve

Syntax: `transition-timing-function: cubic-bezier(x1, y1, x2, y2);`

Tool to make cubic Bezier curves: http://cubic-bezier.com/

### The `steps()` function

Syntax: `transition-timing-function: steps(count, direction);`

The `count` value is an integer that states how many intervals the animation should run through.

The optional `direction` can be set to `start` or `end` (the default). The default `end` means the change happens at the end of the step (pause, then change), and the alternative `start` means the change happens at the start of the step (change, then pause).

### `transition-delay`

Sets the time when the transition starts. 

Syntax: `transition-delay: time;`

The default `time` is `0`. 

## The `transition` shorthand property

Syntax: `transition: property duration timing-function delay;`

## Multiple transitions

Example:

```css
div { transition: border-width 4s, height 500ms, padding 4s; }
```

## Animations

