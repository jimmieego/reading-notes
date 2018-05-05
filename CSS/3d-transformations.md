z-axis: positive value = toward the viewer; negative value = awayf from the viewer.

Use of 3d transformations: 
- adding depth to rollover effects.
- making two-sided “cards” that flip to reveal information on the reverse.

## Rotation around an axis

```css
div {
	transform: rotateX(45deg);
	transform: rotateY(45deg);
	transform: rotateZ(45deg); /* same as the two-dimensional rotate() function */
}
```

Shorthand:

```css
div {
	transform: rotateX(45deg) rotateY(45deg) rotateZ(45deg);
}
```

The `rotate3d()` function:

```css
div.foo {
	transform: rotate3d(1, 1, 0, 45deg); /* x, y, z, angle */
}
```

Here the `x`, `y`, `z` are used to calcuate a direction vector from the origin (0, 0, 0) to (x, y, z). The element will be rotated around this line by the amount specified in the `angle` value.

## Perspective

`perspective()` creates an artificial viewpoint from where you view the object in three- dimensional space, providing the illusion of depth.

Syntax:

```css
div {
	transform: perspective(depth);
}
```

The `depth` is either a length unit or the default keyword `none`. This length sets a “viewpoint” at that distance along the z-axis away from the element’s origin (z = 0).

A low depth value—say, 50px—will make the element appear extremely close to the viewer, with exaggerated dimensions; a value of around 1000px can be considered “normal.”

Note: The `perspective()` function must always be listed *first* when using multiple functions on the `transform` property.

### The `perspective` property

Syntax:

```css
div {
	perspective: 200px; /* works the same way as the function */
}
```

The only difference between the function and the property is that the value supplied to the property applies only to its *child elements*, not to itself.

### The `perspective-origin` property

`perspective-origin` sets the point in 3D space from which you view the element (the line of perspective).

```css
div {
	perspective-origin: 75% 25%; /* x position, y position; default is `center center` */
}
```


## Translation along the axis

Move along the z-axis: `translateZ()`. 

Shorthand function: `translate3d(translateX, translateY, translateZ)`. Example: `translate3d(0, 100%, 1em)`.

## Scaling

Scale along the z-axis: `scaleZ()`. It acts as a multiplier to the value in `translateZ()`.

Example:

```css
div {
	transform: scaleZ(3) translateZ(10px); /* the element appears 30px along the z-axis */
}
```

Shorthand function: `scale3d(scaleX, scaleY, scaleZ)`.

## The transformation origin

Syntax: `transform-origin: x y z;`

For the `z` value, if a negative value is given, the transformation origin is behind the element, which makes it appear in front of its parent; likewise, a positive value places the origin in front of the element, making the element appear behind its parent.

## The `transform-style` property

Syntax: `transform-style: keyword`.

`keyword` can be:

- `flat`: all descendant elements are flattened to the plane of the parent—that is, any transformation functions applied to child elements are ignored.
- `preserve-3d`: descendant elements sit in a separate plane.

## Backface

Syntax: `backface-visibility: state`.

The `state` value can be:

- `visible`: default. The element behaves as if it were transparent, so you will see the reverse of what appears on the front.
- `hidden`: shows nothing.