# Responsive Web Design

Ethan Marcotte

## Chapter 1. Our Responsive Web

Rather than creating disconnected designs, each tailored to a particular device or browser, we should instead treat them as facets of the same experience. We can craft sites that are not only more flexible, but that can adapt to the media that renders them.

Core ingredients of responsive design:

- A flexible, grid-based layout
- Flexible images and media
- Media queries

## Chapter 2. The Flexible Grid

A reset stylesheet can override a browser's default styles for HTML elements, which gets all browsers working from a consistent baseline.

Every aspect of the grid - the rows and columns, and the modules draped over them - can be expressed as *proportions* of their containing element, rather than in unchanging, inflexible pixels. 

Formula: `target / context = result` (`em`)

### Flexible Margins and Padding

1. When setting flexible **margins** on an element, your context is the width of the element’s *container*.
2. When setting flexible **padding** on an element, your context is the width of the element *itself*. Which makes sense, if you think about the box model: we’re describing the padding in relation to the width of the box itself.

## Chapter 3. Flexible Images

```css
img,
embed,
object,
video {
	max-width: 100%;
}
```

The `max-width: 100%` forces the image's width to *match* the width of its container. It can also apply to most fixed-width elements, like video and other rich media.

Also use CSS media queries to apply different image sizes for different resolution ranges.

### Overflow

Clip off excess image:

```css
.feature {
	overflow: hidden;
}
.feature img {
	display: block;
	max-width: auto;
}
```

Note: `overflow` is generally less useful than scaling the image via `max-width`.

## Chapter 4. Media Queries

Examples:

```css
@media screen and (min-width: 1024px) {
	body {
		font-size: 100%;
	}
}
```

```css
@import url("wide.css") screen and (min-width: 1024px);
```

```html
<link rel="stylesheet" href="wide.css" media="screen and (min-width: 1024px)" />
```

**display area**: the browser's viewport.
**rendering surface**: the entire display.

We can chain multiple queries together with the `and` keyword:

```css
@media screen and (min-device-width: 480px) and (orientation: landscape) {}
```

Research your target devices and browsers thoroughly for the query features they support, and test accordingly.

```html
<meta name="viewport" content="initial-scale=1.0, width=device-width" />
```

You can also use `max-width` to contraint your page design.