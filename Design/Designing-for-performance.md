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