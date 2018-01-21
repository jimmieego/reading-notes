## Chapter 2. Navigation
- Think about content through a three-part, mobile-first framework:
	1. Identify the content critical to the smaller screen.
	2. Consider that content to be the information accessible to all your readers, regardless of how wide (or small) their screen happens to be.
	3. If there's additional information you'd like to include on wider viewports, consider it as an *enhancement*.
- Common pattern: use the hamburger icon and drawer to conceal navigation in small screens.
	- The downside of being able to show a lot of options is that you can show a lot of options (in the drawer navigation menu).
	- Need to prioritize and focus on only the most important tasks users want to accomplish on small screens.
- If we’re collapsing or hiding something because it doesn’t “fit,” let’s instead see that as an opportunity to stop and ask if there’s a larger issue at play: that is, if we’re hiding or removing an element because it doesn’t have value on smaller screens, can we simplify the design and content of that element until it works on smaller screens? Or, alternately, maybe it doesn’t have value for any screen?
- We should stop trying to make complex, widescreen-de- signed elements play nice on smaller screens—instead, we should consider the small-screen user’s needs first.
- There’s nothing inherently wrong with the hamburger icon itself — but assuming it’s a safe default for every responsive navigation system can be problematic. Need to do testing. 
- Alternate patterns:
	- Progressive reveal: As the design gets wider, more links are gradually, progressively revealed. Use JavaScript to measure the width of the browser’s viewport and then, based on its width, shows or hides certain links in each menu. Key elements are kept visible at all times.
	- Adapt the layout: Not hide or conceal the navigation, but simply change its layout, particularly on the homepage. 

## Chapter 3. Images and Videos
### Inline images
Images can render at whatever dimensions they want, as long as their width never exceeds the width of their containing element.

```css
img {
	max-width: 100%;
}
```

### Fluid videos
Resize video/object proportionally:

```html
<div class="player">
	<video src="video.mp4" height="168" width="300"></video>
</div>
```

```css
.player {
	position: relative; /* Positioning context: any element absolutely positioned inside the context of this container will now be positioned relative to .player, rather than the viewport. */
	padding-top: 50%;
}
.player video {
	position: absolute;
	left: 0;
	top: 0;
	height: 100%;
	width: 100%;
}
```

Note: Set aspect ratio (height/width %) to `padding-top`. Percentages on `padding-top` and `padding-bottom` are relative to the *width* of the containing block, not the height.

### Flexible backgrounds

`background-size` allows us to specify the size of background image. We can even define `background-size` in percentages, scaling the image relative to the dimensions of its container. 

- `background-size: cover`: The browser will evaluate the width and height of the background image, and find the smaller of the two values. It will then scale the image proportionally, ensuring that the smaller dimension - either the width or the height - covers its container. It may occasionally hide parts of the image from view. 
- `background-size: contain`: This ensures the entire background is always visible within its container. 

### Responsive images
Flexible images could be invisible overhead as small screens will not be able do display the extra pixels. 

Use `srcset` attribute inside `<img>` tag to provide options of multiple images that could be loaded, depending on pixel densitities like `2x` and `3x` or scales like `1440w` and `720w`. The browser selects the image best suited to the density of the display or the native width of the image.

`sizes` attribute for `<img>` tag, examples: 
- `(min-width: 50em) 250px`: if the viewport has a minimum width of `50em`, the image will be `250px` wide.
- `(min-width: 35em) 33vw`: a `vw` is 1% of the viewport's width.
- `100vw`: the image will occupy the full width of the viewport.

While we can resize images with a mixture of `max-width: 100%`, `srcset`, and `sizes`, it's worth remembering that the images are actually documents themseleves. We should ensure the message survives at any scale.

A `<picture>` element contains any number of `<source>` elements, and exactly one `<img>`. On each `<source>`, there's a media query inside the `media` attribute and a `srcset` attribute. The browser loops through each of the `<source>` elements until it finds one whose media query matches the conditions in the browser. Upon finding a match, it will send that `<source>`'s `srcset` to the `<img>` element and load it. If there aren't any matches, the browser will just load the `<img>`.

The `<source>` element can have a `type` attribute for specifying the image file format (e.g., `type="image/svg+xml"`).

## Chapter 4. Responsive Advertising
Most ads on the web are fixed-width.

### Conditional loading
Load only what we need at any given viewport, rather than hiding the excess with CSS. Identify the ads best suited fro each breakpoint, and then load them only if the design can accommodate them. 

Ajax-Include pattern:

```html
<div class="sb"
	data-append = "/include/sidebar-contents.html"
	data-media = "(min-width: 63.75em)"></div>
```

### Rethinking the hierarchy
Resposition the advertisements: The placement of an advertisement would be determined by the width of the page. When the site is a single column, insert ads into sensible points in the content flow. As the layout widened to two columns, the ad would move from its initial position and stick to the top of that new column. Similarly, when a third column appeared at the widest breakpoint, the ad would shift again. 

```html
<div data-adname="MAIN_AD" class="ad-slot-a"></div>

<div data-adname="MAIN_AD" class="ad-slot-b"></div>

<div data-adname="MAIN_AD" class="ad-slot-c"></div>
```

1. JavaScript begins by looping through all `div`s that share a `data-adname` value, and looking for the first one that’s set to `display: block`.
2. Once it’s found, the JavaScript inserts the ad into that slot.
3. Whenever the browser window resizes or the device’s orientation changes, the JavaScript starts the process over again: looking for the visible block, and moving the ad into that container.


### New models
- Treat ads as small-scale responsive layouts instead of fixed, inflexible blocks. Reposition these elements within a flexible, responsive canvas. 


## Chapter 5. Designing the Infinite Grid

