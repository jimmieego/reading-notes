# Responsible Responsive Design

Scott Jehl

## Introduction

A responsible responsive design equally considers the following throughout a project:

- **Usability**: The way a website’s user interface is presented to the user, and how that UI responds to browsing conditions and user interactions.
- **Access**: The ability for users of all devices, browsers, and as- sistive technologies to access and understand a site’s features and content.
- **Sustainability**: The ability for the technology driving a site or application to work for devices that exist today and to continue to be usable and accessible to users, devices, and browsers in the future.
- **Performance**: The speed at which a site’s features and content are perceived to be delivered to the user and the efficiency with which they operate within the user interface.

## Responsible Design

Responsive design's core tenets: fluid grids, fluid images, and media queries.

Two responsible tenets: **usability** and **accessibility**.

The number of characters per line in a column of text for immersive reading is widely thought to fall between **45** and **75** characters, including spaces.

It is often helpful to compile the multiple configurations of each modular components in isolation, in order to test its usability and document its variations in one place.

### Progressive disclosure

Hide portions of content, but provide interface cues so that users can view it when they wish.

### Responsive table

- Reflow the table from a multile-column view to a list view; each cell becomes its own row, with a row header to its left. This pattern falls short when you need to compare data points across rows.
- Horizontal scrolling and allow the user to show/hide columns.

### Touch

- Make sure any content that offers mouse-centric interactivity (like `hover`) is also accessible in browsers where a mouse pointer may not exist.
- Don't assume touch will be used, but design as if it will be.
  - Apple suggests 44 x 44 px as the minimum size for usable buttons.
- Ensure there's always a click-and-keyboard-based interface for interaction. Think of touch gestures as a nice-to-have enhancement on top of broadly supported input modes.

## Sustainable Detection

**Features**: CSS properties and JavaScript APIs
**Constraints**: Viewport size, unpredictable connectivity, off-line use

Designing for features and constraints allows us to see how patterns that may otherwise seem distinct are shared across devices, and to build in a modular manner to create unique experiences that feel appropriate to each device.

**Mobile first**: Start small and layer in more complex layout as space permits. This helps prioritize content.

A mobile-first responsive stylesheet begins with styles that are shared across all experiences, forming the foundation of the smallest screen layout. These styles are followed by a series of mostly `min-width` media queries to scale that layout up to greater viewport sizes and pixel depths.

### Use Modernizr to run feature tests

When Modernizr tests run, the framework retains a JavaScript property, stored on the globally available `Modernizr` object, of that test's name that equals `true` if it passes or `false` if it doesn't. When a test passe, Modernizr also adds a class of that test's name to the `html` element, which you can then use within your CSS selectors to qualify the user of certain features.

### `@supports` in CSS

By passing any CSS property and value pair (e.g., `display: flex`) to the `@supports` rule, you can define entire style blocks to apply only in browsers that implement that CSS feature.

### polyfills

The decision to use a polyfill should be based on three main points:

- how much the feature improves your audience’s user experience,
- the cost to performance of including the polyfill in a page,
- its ability to one day be removed seamlessly from your codebase.

## Performance

### Page-loading process

**Critical path**: the events that take place from the moment a page is requested to the moment that page is usable.

CSS works best when all styles relevant to the initial page layout are loaded and parsed *before* an HTML document is rendered visually on a screen.

JavaScript behavior is often able to be applied to page elements *after* they’re loaded and rendered.

**Blocking**: By default, browsers wait to render a page’s content until assets like CSS and JavaScriptfinish loading and parsing.

Note: images are non-blocking asset.

We need to reduce the number of blocking requests.

### Chrome developer tools

When it comes to page-load performance, two panes are especially useful: **Network** and **Timeline**.

### Perceived performance

**Perceived load time** is often more important to us than total page-load time.

One-second page load has emerged as a de facto standard goal.

Test tools:

- [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
- [WebPagetest](https://www.webpagetest.org/): the lower the Speed Index score, the better; 1000 is a great score to shoot for.

### Performance budget

A performance budget is a number, or set of numbers, used as a guideline for whether you can afford a particular code addition to a codebase, or whether an existing site’s performance needs to improve. The numbers can be page transfer weight or perceived load time.

Performance is not just developmental concern, it's a fundamental component of the user experience.

## Deliver

### Prepare files for web delivery

- Optimize image files: [ImageOptim](https://imageoptim.com/howto.html)
- Concatenate text files: `cat foo.js bar.js > foobar.js`
- Minify text files
- Compress text files: Gzip makes text files smaller for transfer between server and browser.
- Caches
  - Browser's default cache: automatically store any files it requests so that the next time those files are requested, it can avoid a network request and instead use the local copy. Use response headers to configure the ways in which any given files should be cached.
  - HTML 5 offline cache: `<html manifest="example.appcache">`. The contents of the `example.appcache` file tell the browser which assets it should cache for offline use and which assets it should always request over the network. Application cache and other related browser features like local storage and Service Worker API make it possible to specify how and which features of a site should work offline and which ones require a web connection.

Use [Grunt](https://gruntjs.com/) to automate tasks.

### Deliver HTML

**Deferred or lazy loading**: Identify what portions of the content are absolutely necessary and load the rest later on, after the essentials have been served.

If a piece of supplementary content is already accessible in its own dedicated place elsewhere on the site, that piece may be a good candidate for deferred loading.

Configuring our pages to serve critical content first can lead to a faster initial page load. To load auxiliary content, we can then use JavaScript after the page is presented to the user.

### Deliver CSS

- Approach A: one big stylesheet containing inline media queries.
- Approach B: separate, media-specific files

  ```html
  <link href="medium.css" media="(min-width: 35em) rel="stylesheet""
  ```

  Note: Browsers will still request all stylesheets, regardless of whether their media attributes match or note. Some modern browsers will give inapplicable stylesheets lower priorities and won't block page rendering.

- Approach C: everything inline.

  Note: inlining styles into the HTML removes a browser’s ability to cache those styles as its own asset for future page loads.

- A hybrid approach

  Inline only the CSS critical for rendering content in the initial view, and load the rest in a non-blocking way. Critical CSS is the subset of CSS rules required to render the top portion of a page at a given viewport size.

  JavaScript has a function called `loadCSS` which loads CSS files asynchronously so that they don't block page rendering. It's recommended to place the script with `loadCSS` *after* the `<style>` element, which allows the JavaScript to insert the site's full CSS after the inline CSS, avoiding potential specificity conflicts.

### Deliver images

All browsers request images asynchronously, or without blocking page rendering, by default.

#### Data URI

**Data URI** embeds an image’s (or any file’s) data directly into a string of gibberish that you can use in place of an external reference to that file, removing the need to make a request to the server for that asset. 

Data URI Syntax:

```html
data:[<MIME-type>][;charset=<encoding>][;base64],<data>
```

Reserve data URIs for universal assets that apply across devices and breakpoints.

#### Responsive images with HTML

```html
<picture>
  <source media="(min-width: 45em)" srcset="large.jpg 45em, large-2x.jpg 90em">
  <source media="(min-width: 18em)" srcset="med.jpg 18em, med-2x.jpg 36em">
  <img srcset="small.jpg 8em, small-2x.jpg 16em" alt="...">
</picture>
```

A `picture` element contains a series of `source` elements followed by an `img` element.

The `source` elements are listed in order of largest first, with media attributes specifying the maximum viewport size at which they should be applied. 

A browser will iterate over the `source` elements in order of appearance and stop when it encounters a `source` with a matching media attribute, then set the `img` element’s source to a URL specified in the `source` element’s `srcset` attribute. If no source elements end up matching, the `img` element’s own attributes (such as `srcset`) will be used to determine its source.

`srcset` is a new attribute to contain one or more potential source URLs (comma-delimited) for an image. The browser can decide the most appropriate asset based on any criteria the browser deems relevant.

You can pair each value with a description of the image’s dimensions (using `w` and `h` units representing pixel measurements of the image asset itself).

```html
<img srcset="imgs/small.png 400w, imgs/medium.png 800w" alt="...">
```

The new `sizes` attribute let's us suggest the size at which an image will be rendered in the layout at a given media query breakpoint. Note that these widths won’t actually apply to the image; they’re merely cues to allow the browser to render the image as close to its intended dimensions as possible.

```html
<img
srcset="imgs/small.png 400w, imgs/medium.png 800w" sizes="(max-width: 30em) 100%, 50%" "alt="...">
```

- `(max-width:30em)100%`: When the viewport is `30em` or narrower, the image’s width will be `100%` of the viewport’s width.
- `50%`: Otherwise, if the viewport is wider than `30em`, the image’s width will be `50%` of the viewport’s width.

`type`: can be `"image/svg+xml"`, `"image/webp"` (a new, highly optimized image format).

#### SVG

SVG as an img:

```html
<picture>
  <source type="image/svg+xml" srcset="star.svg">
  <img srcset="star.png" alt="...">
</picture>
```

SVG in html: To embed SVG in a document, just paste that SVG markup anywhere in the `body` of your page and it’ll render in any supporting browser.

SVG as an object:

```html
<object data="star.svg" type="image/svg+xml">
   ...Fallback content goes here.
</object>
```

SVG as background image:

```css
.star {
  background: url(star.svg);
}
```

### Deliver fonts

FOUT: Flash of unstyled text. It happens whenever an HTML page is displayed before its custom web fonts have finished loading.

Recommendation: Convert each of your custom fonts into data URIs and packing them into a single CSS file along with their `font-face` definitions. Use the `loadCSS` in JavaScript to load fonts.css in a non-blocking manner. 

### Deliver JavaScript

Consider JS a tertiary enhancement. Alaways try to determine whether behavior or presentation can be achieved with HTML and CSS alone. 

Question whether a library is necessary at all. For example, `querySelectorAll()` in JavaScript can query the DOM for elements using CSS selectors, just as in jQuery.

Consider a simple DOM framework or a custom library build.

#### Options for loading JavaScript:

- Use the `script` element within the `head` of a document. Scripts referenced this way delay page rendering until they have finished loading and executing.
- Inline JavaScript in the `head`. This is good for the small, critical portion of JavaScript. Any script embedded directly in the page can't be cached as an individual file, so it will re-download with every new page that includes it.
- Place `script` elements at the end of an HTML document. This allows content to load and render as soon as possible, and force scripts to load and execute after the content itself has been parsed and rendered.
- `async` attribute in `script`: instruct the browser to load a JavaScript file in parallel while the HTML is stll loading. This does not guarantee that multiple scripts will execute in the order they're specified in the page source.
- `defer` attribute in `script`: execute the script after the HTML has finished loading.
- Dynamic loading: place a bit of JavaScript inline in the page and use that script to append additional `script` elements, which will download and execute in parallel. The `insertBefore` method is the safest and most reliable. Note that this approach does not ensure that scripts will execute in the order they are requested.

```html
  <head>
    <script>
      var myJS = document.createElement("script");
      myJS.src = "myScript.js";
      var ref = document.getElementByTagName("script")[0];
      ref.parentNode.insertBefore(myJS, ref);
    </script>
  </head>
```

### Deliver enhancement

Two-tiered responsive solution: depending on their capabilities, browsers receive either a functional, simple HTML-only experience or the enhanced version. Use feature tests to ensure that we only apply enhanced scripting and styles in places that can understand them.

Qualified asset loading:

```javascript
if("querySelector" in document) {
  document.documentElement.className += "enhanced";
  loadJS("myScript.js");
}
```

Within the `head`, inline both critical CSS and JavaScript to help load additional scripts, styles, and fonts in a qualified manner.