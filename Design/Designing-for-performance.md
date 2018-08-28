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