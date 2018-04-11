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

### Percevied performance

**Perceived load time** is often more important to us than total page-load time.

One-second page load has emerged as a de facto standard goal.

Test tools:

- [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
- [WebPagetest](https://www.webpagetest.org/): the lower the Speed Index score, the better; 1000 is a great score to shoot for.

### Performance budget

A performance budget is a number, or set of numbers, used as a guideline for whether you can afford a particular code addition to a codebase, or whether an existing site’s performance needs to improve. The numbers can be page transfer weight or perceived load time.

Performance is not just developmental concern, it's a fundamental component of the user experience.

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

**Data URI** embeds an image’s (or any file’s) data directly into a string of gibberish that you can use in place of an external reference to that file, removing the need to make a request to the server for that asset.