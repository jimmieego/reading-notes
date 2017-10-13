## Detect when the DOM is ready
We can use `requestAnimationFrame()` to repeatedly check if the `body` element and any other target element exist, and then run a function once it does. 

```javascript
var ready = function () {

    // If the body element and the #main element exist
    if (document.body && document.querySelector('#main')) {
        // Run your code here...

        // Return so that we don't call requestAnimationFrame() again
        return;
    }

    // If the body element isn't found, run ready() again at the next pain
    window.requestAnimationFrame(ready);
};

// Initialize our ready() function
window.requestAnimationFrame(ready);

```

## Debouncing events
The `requestAnimationFrame()` sets up a callback function. It runs the next time a page paint is requested.

```javascript
var timeout;

// Listen for resize events
window.addEventListener('scroll', function ( event ) {

    console.log( 'no debounce' );

    // If there's a timer, cancel it
    if (timeout) {
        window.cancelAnimationFrame(timeout);
    }

    // Setup the new requestAnimationFrame()
    timeout = window.requestAnimationFrame(function () {

        // Run our scroll functions
        console.log( 'debounced' );

    });

}, false);
```