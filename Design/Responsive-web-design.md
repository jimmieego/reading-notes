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

## Chapter 5. Becoming Responsive

At its most basic level, responsive design is about serving one HTML document to countless browsers and devices, using flexible layouts and media queries to ensure that design is as portable and accessible as possible.

Responsive web design isn’t intended to serve as a replacement for mobile web sites.

How do you know if responsive design is right for you?

- Know the users' goals
- Design for *mobile first*
- Ask this during site planning: *How does this content or feature benefit the mobile users?*

### Workflow

1. Identify the breakpoints
2. Iterative, collaborative design.   
  Prototype before the designs are final to get beyond the pixel limitations of design tools. Begin building a design that can flex and grow inside a changing browser window. 
3. The interactive design review.  
  The goal is to close the gap between the traditional "design" and "development" cycles, to let the two groups collaborate more closely to produce a finished, responsive design.

### Be more responsible

In general, responsive design is about starting from a reference resolution, and using media queries to adapt it to other contexts. We should build our stylesheet with "mobile first" in mind, rather than defaulting to a desktop layout. We should begin by defining a layout appropriate to smaller screens, and then use media queries to progressively enhance our design as the resolution increases.

Use `min-width` media queries to scale the design *up*.

### Progressive enhancement

Progressive enhancement builds documents for the least capable or differently capable devices first, then moves on to enhance those documents with separate logic for presentation.