# Designing for Performance

Lara Callender Hogan

## Chapter 1. Performance Is User Experience

## Chapter 2. The Basics of Page Speed

We’ll aim to optimize for:

- The number of resources (like images, fonts, HTML, and CSS) loaded on a page
- The file size of these resources
- The perceived performance of your site by your users

### How Browsers Render Content

1. DNS lookup and browser sends request to server
2. Server decodes request and sends back content requested

Optimizing the size and number of requests that it takes to create your web page will make a tremendous impact on your site’s page load time.

Use waterfall charts to assess how well your page is loading in combination with measuring your total page weight and the perceived performance of your page.

### Perceived Performance

Users’ perception of speed will be based on how quickly they start to see content render on the page, how quickly it becomes interactive, and how smoothly the site scrolls.

By default, CSS is treated as a render-blocking resource. Use media types and media queries to indicate which parts of your CSS can be non-render-blocking: 

```html
<link href="main.css" rel="stylesheet">
<link href="print.css" rel="stylesheet" media="print">
<link href="big-screens.css" rel="stylesheet" media="(min-width: 61.5em)">
```

JavaScript blocks DOM construction unless it is declared as asynchronous.

Optimize the critical rendering path:

- Asynchronously load content
- Prioritize requests for “above the fold” content
- Follow best practices for loading CSS and JavaScript
- Cache assets for returning users
- Ensure that any primary actions for the page are available to the user as quickly as possible

Repaints are expensive operations for browsers, and will make your page feel sluggish.

## Chapter 3. Optimizing Images

- Finding the right balance of file size and quality for each image
- Looking for ways to reduce the total number of image requests on your site
- Optimizing your site’s image creation workflows for performance improvements

|Format |Best for | Optimization options|
|-------|---------|---------------------|
|JPEG|Photos, images with many colors|Decrease quality, export as progressive, reduce noise|
|GIF|Animations|decrease dithering, decrease number of colors, increase horizontal patterns, reduce vertical noise |
|PNG-8|Images with few colors|decrease dithering, decrease number of colors, increase horizontal and vertical patterns|
|PNG-24|Partial transparency|reduce noise, reduce number of colors|

- *Baseline JPEG*: full-resolution, top-to-bottom scan of an image.
- *Progressive JPEG*: appear all at once at low quality; then this low-quality version of the image is replaced with versions of progressively higher quality.

Serving an image that is larger than necessary and scaling it down within an image tag will negatively impact your page load time, as you are forcing the user to download more bytes than needed.

### Replacing image requests

- Combine images into sprites
- Replace image files with CSS3, data URIs, or SVG versions

Use CSS to replace images. For example:

```css
/* Adding a basic bevel gradient */
button {
    background-image: linear-gradient(to bottom, #FFF, transparent);
    background-color: #DDD;
    border: 1px #DDD solid;
}
```

If you find that your user interface does become sluggish, especially upon scrolling, you may have a CSS3 or JavaScript repaint issue and will want to diagnose what’s causing it using tools from [JankFree.org] (http://jank-free.org/).

## Optimizing Markup and Styles

### Cleaning HTML

When looking at your site’s HTML, watch for:

- Embedded or inline styles that should be moved to a stylesheet
- Elements that have no need for special styling
- Old, commented-out code that can be removed

### Cleaning CSS

Watch for:

- Element names that don’t have semantic meaning
- `!important` declarations
- Browser-specific hacks
- Lots of selector specificity
- Unused styles

Look through your stylesheets for opportunities to combine or condense these styles, as they will help with both the performance and maintainability of your code.

If you have many icons or other small images used throughout the site, a sprite can be a huge help in optimizing requests.

Consider the number of stylesheet images called and whether they can be condensed or replaced with CSS or SVG.

Always start with the smallest, lightest selector possible and add specificity from there. Reducing specificity means that it will be easier to override styles with the naturally cascading power of CSS, rather than slip in additional weight or `!important` rules.

### Optimizing web fonts

```css
@font-face {
    font-family: 'FontName';
    src: url('fontname.woff') format('woff');
}

body {
    font-family: 'FontName', Fallback, sans-serif;
}
```

The most important action you can take when applying web fonts is to be deliberate about their uses. Document when and how to use a particular font weight so that others working on your site can repurpose this markup and understand when it is appropriate to apply a font weight.

### Creating repurposable markup

The more patterns are repurposed, the higher the chances are that the styles and other assets will already be cached, the shorter your stylesheets will be, and the faster the site will load.

### Additional markup considerations

Putting stylesheets in the `<head>` allows content to be displayed progressively to the user because the browser isn’t still looking for more style information.

Avoid using `@import`, which can significantly increase page load time.

JavaScript files should be loaded at the end of the page and loaded asynchronously whenever possible. This will allow other page content to be displayed to the user more quickly, as JavaScript blocks DOM construction unless it is explicitly declared as asynchronous.

```html
<script src="main.js" async></script>
```

Anything that loads late and affects page layout can cause content to shift, surprising the user; build in placeholders to make sure the page looks and feels stable as it loads.

In terms of script performance, watch your waterfall charts to make sure that your JavaScript files are loading *after* your other content and not blocking other downloads or rendering important pieces of the page.

gzip is great for all kinds of text files like stylesheets, HTML, JavaScript, and fonts. The only exception to this is WOFF font files, which come with built-in compression.

### Caching assets

There are two kinds of caching parameters that can be included in a response header:

- Those that set the time period during which a browser can use its cached asset without checking to see if there’s a new one available from the server (`Expires` and `Cache-Control: max-age`).
- Those that tell the browser information about the asset's version so it can compare its cached version to the one that lives on the server (`Last-Modified` and `ETag`).

All static assets (CSS files, JavaScript files, images, PDFs, fonts, etc .) should be cached.

## Chapter 5. Responsive Web Design

### Loading the correct image size

Simply setting `display: none` to an element will not prevent a browser from downloading the image. The same goes for applying `display: none` to an element with a `background-image`; the image will still be downloaded. Instead, if you want to hide an image from displaying with CSS in a responsive design, you can try hiding the *parent* element of the element with a `background-image`. Alternatively, you could apply different media queries to tell the browser which `background-image` is appropriate to download at which screen size.

The `picture` element in HTML:

```html
<picture>
    <source media="(min-width: 800px)" srcset="big.png 1x, big-hd.png 2x">
    <source media="(min-width: 600px)" srcset="medium.png 1x, medium-hd.png 2x">
    <img src="small.png" srcset="small-hd.png 2x" alt="Description">
</picture>
```

The first `source` to match, top to bottom, is the resource that gets picked for the browser to download.

The `type` attribute of the `picture` element:

```html
<picture>
    <source type="image/svg+xml" srcset="pic.svg">
    <img src="pic.png" alt="Description">
</picture>
```

The `size` attribute of the `picture` element:

```html
<img srcset="small.jpg 400w, medium.jpg 800w, big.jpg 1600w" sizes="(min-width: 1000px) 33.3vw, 100vw" src="small.jpg" alt="Description">
<!-- at larger screens, the image will be shown at 33% of the viewport, but the default width of the image is 100% of the viewport -->
```

### Fonts

Load the custom font file only on larger screens:

```css
@font-face {
    font-family: 'FontName';
    src: url('fontname.woff') format('woff');
}

body {
    font-family: Georgia, serif;
}

@media (min-width: 1000px) {
    body {
        font-family: 'FontName', Georgia, serif;
    }
}
```

### Mobile first approach

Consider the smallest screen sizes first. Reorder the CSS to deliver small screen styles first, and use progressive enhancement to add content and capabilities as screen sizes get larger. From there, you can make decisions about how to share larger assets on larger screens, reflow content in your hierarchy, and continue to be deliberate about performance in your overall user experience.

## Chapter 6. Measuring and Iterating on Performance

Speed Index: The average time at which visible parts of the page are displayed. It helps you benchmark the perceived performance of your page, since it will tell you how quickly the “above the fold” content is populated for your users. The smaller the Speed Index score, the better.

Benchmarking performance as it changes over time, especially when you can directly attribute it to work being done on your site, will empower you and others to make smart decisions about aesthetics and performance.