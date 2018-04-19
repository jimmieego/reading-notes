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

