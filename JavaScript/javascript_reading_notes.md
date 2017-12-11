## Get URL Variables

```javascript
function getQueryVariable(variable)
{
       var query = window.location.search.substring(1);
       var vars = query.split("&");
       for (var i=0;i<vars.length;i++) {
               var pair = vars[i].split("=");
               if(pair[0] == variable){return pair[1];}
       }
       return(false);
}
```

Usage:

Example URL:
http://www.example.com/index.php?id=1&image=awesome.jpg

Calling `getQueryVariable("id")` - would return "1".
Calling `getQueryVariable("image")` - would return "awesome.jpg".


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

## Compare two arrays (objects)
```javascript
var isEqual = function (value, other) {

    // Get the value type
    var type = Object.prototype.toString.call(value);

    // If the two objects are not the same type, return false
    if (type !== Object.prototype.toString.call(other)) return false;

    // If items are not an object or array, return false
    if (['[object Array]', '[object Object]'].indexOf(type) < 0) return false;

    // Compare the length of the length of the two items
    var valueLen = type === '[object Array]' ? value.length : Object.keys(value).length;
    var otherLen = type === '[object Array]' ? other.length : Object.keys(other).length;
    if (valueLen !== otherLen) return false;

    // Compare two items
    var compare = function (item1, item2) {

        // Get the object type
        var itemType = Object.prototype.toString.call(item1);

        // If an object or array, compare recursively
        if (['[object Array]', '[object Object]'].indexOf(itemType) >= 0) {
            if (!isEqual(item1, item2)) return false;
        }

        // Otherwise, do a simple comparison
        else {

            // If the two items are not the same type, return false
            if (itemType !== Object.prototype.toString.call(item2)) return false;

            // Else if it's a function, convert to a string and compare
            // Otherwise, just compare
            if (itemType === '[object Function]') {
                if (item1.toString() !== item2.toString()) return false;
            } else {
                if (item1 !== item2) return false;
            }

        }
    };

    // Compare properties
    if (type === '[object Array]') {
        for (var i = 0; i < valueLen; i++) {
            if (compare(value[i], other[i]) === false) return false;
        }
    } else {
        for (var key in value) {
            if (value.hasOwnProperty(key)) {
                if (compare(value[key], other[key]) === false) return false;
            }
        }
    }

    // If nothing failed, return true
    return true;

};
```

## Add items to an array
You can use the `push()` method to add items to an array.

```javascript
var sandwiches = ['turkey', 'tuna', 'blt'];
sandwiches.push('chicken', 'pb&j');
// returns ['turkey', 'tuna', 'blt', 'chicken', 'pb&j']
```

You can use `Array.prototype.push.apply()` to merge two or more arrays together. It merges all subsequent arrays into the first.

```javascript
var sandwiches1 = ['turkey', 'tuna', 'blt'];
var sandwiches2 = ['chicken', 'pb&j'];
Array.prototype.push.apply(sandwiches1, sandwiches2);
// returns ['turkey', 'tuna', 'blt', 'chicken', 'pb&j']
```