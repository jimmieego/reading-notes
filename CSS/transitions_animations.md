# CSS Transitions and Animations

Transitions only take effect when the property they are applied to changes value. Animations are explicitly executed when applied to an element.

## Transitions

A *transition* is an *implicit* animation that moves a property between two states. For a transition to occur, four conditions must be in place: an initial value, an end value, the transition itself, and a trigger. All transitions act in reverse when the trigger is no longer active.

Example:

```css
div {
    background-color: black;
    transition: background-color 2s;
}

div:focus,
div:hover { 
	background-color: silver; 
}
```

Note: The transition instructions are attached to the normal state to avoid duplication in other states.

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

The process of creating animations:

1. define the properties and timings (keyframes);
2. add the animation controls to the elements that will be animated.

### Define keyframes

*Keyframes* are points that set the start and end of a transition. Keyframes can be reused throughout the stylesheet within multiple declarations.

Syntax:

```css
@keyframes name {
	selector {
		property: value;
	}
}
```

The `selector` sets the position along the duration of the animation that the keyframe will occur. The usual value here is a percentage value. You can also use keyword `from` for 0 percent and `to` for 100 percent.

Example:

```css
@keyframes expand {
	from { border-width: 4px; }
	50% { border-width: 12px; }
	to {
		border-width: 4px;
		height: 100%;
		width: 100%;
	}
}
```

Note that inheritance operates on individual keyframes, so if you want a change to persist between frames, you need to specify it in each frame.

### Apply animation control

#### `animation-name`

The `animation-name` property refers to an animation that’s been defined with the `@keyframes` rule.

Syntax: `div { animation-name: name; }`

#### `animation-duration`

Syntax: `div { animation-duration: time; }`

#### `animation-timing-function`

Syntax: `div { animation-timing-function: value; }`. 

The `value` can be keywords (`ease`, `linear`, `ease-in`, `ease-out`, and `ease-in-out`), the `cubic-bezier()` function, or the `steps()` function.

#### `animation-delay`

Syntax: `div { animation-delay: time; }`

Note: negative values of `time` cause the animation to “skip” by that amount.

#### `animation-iteration-count`

Sets the number of repetitions.

Syntax: `div { animation-iteration-count: count; }`

The `count` can be a whole number or `infinite`. Default value is 1.

#### `animation-direction`

Sets whether the animation always plays in one direction or alternates playing forward and backward.

Syntax: `div { animation-direction: keyword; }`

The `keyword` can be `normal` or `alternate`. The `normal` always plays the animation forward. The `alternate` plays the animation from start to finish and then plays in reverse before starting over again.

#### `animation-fill-mode`

Sets how the element appears outside of the animation cycle.

Syntax: `div { animation-fill-mode: keyword; }`

The `keyword` can be:

- `none`: default.
- `backwards`: the declarations specified in the `0%` (or `from`) keyframe will be applied to the element before the animation begins.
- `forwards`: the declarations in the `100%` (or `to`) keyframe will be applied when the animation ends.
- `both`: the `0%` declarations will apply before the animation and the `100%`, after.

#### `animation-play-state`

Sets whether an animation is active.

Syntax: `div { animation-play-state: keyword; }`

The `keyword` can be:

- `running`: means the animation is playing.
- `paused`: means the animation is not playing.

### The `animation` shorthand

Syntax:

```css
div {
	animation: name duration timing-function delay iteration-count direction fill-mode play-state;
}
```

### Multiple animations

You can add multiple animations to an element using a comma-separated list. This method works for each of the subproperties and the shorthand property.

Example:

```css
#animation {
	animation-name: first-anim, second-anim; 
	animation-duration: 6s, 1.25ms; 
	animation-delay: 0, 750ms;
}

#animation2 {
	animation: first-anim 6s, second-anim 1.25ms 750ms;
}
```