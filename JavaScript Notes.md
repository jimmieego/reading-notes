# JavaScript Notes

## Select elements
- Select an individual element: `getElementById()`, `querySelector()`
- Select multiple elements (nodelists): 
    - `getElementsByClassName()`
    - `getElementsByTagName()`
    - `querySelectorAll()`
- Transverse between element nodes: `parentNode`, `previousSibling`, `nextSibling`, `firstChild`, `lastChild`

# Attribute methods
- `getAttribute()`
- `hasAttribute()`
- `setAttribute()`
- `removeAttribute()`
- `className`: get or set the value of the class attribute
- `id`: get or set the value of the id attribute

# DOM manipulation
`appendChild()`
`removeChild()`
`replaceChild()`
`insertBefore()`
`createElement()`
`createTextNode()`

# Event
- Using HTML event handlers is bad practice. For example, do not use `<a onclick="hide()">`. It is better to separate JavaScript from the HTML.
- Traditional DOM event handlers: `element.onevent = functionName;` You can only attach one function to each event handler. The event name is preceded by the word “on”.
- Event listeners: `element.addEventListener('event', functionName, [,Boolean]);` The Boolean indicates event capturing phase or bubbling phase, and is usually set to false. The event name is not preceded by the word “on”. There is a function called removeEventListener() which removes the event listener from the specified element.
- Use parameters: `element.addEventListener('event', function(){functionName(parameters)}, false);` The named function that requires the arguments lives inside the anonymous function.
- `mousedown` is equivalent to `touchstart`
- `mousedup` is equivalent to `touchend`
- `keydown`: fires when the user presses any key on the keyboard.
- `keypress`: fires when the user presses a key that would result in a character being shown on the screen. For example, this event would not fire when the user presses the arrow keys, whereas the keydown event would.
- `keyup`: fires when the user releases a key on the keyboard. The keydown and keypress events fire before a character shows on screen, whereas keyup fires after it appears.
- Get the letter or number from `keydown` or `keypress` events: `String.fromCharCode(event.keycode);`

# Position
- `screenX` and `screenY` indicate the position of the cursor within the entire screen on the monitor, measuring from the top left corner of the screen (rather than the browser).
- `pageX` and `pageY` indicate the position of the cursor within the entire page. The top of the page may be outside of the viewport so even if the cursor is in the same position, page and client coordinates can be different.
- `clientX` and `clientY` indicate the position of the cursor within the browser’s viewport. If the user has scrolled down and the top of the page is no longer in view, it will not affect the client coordinates.

# Promises
Style 1:
```javascript
fetch(url).then(function(dogBiscuits) {
  dogBiscuits.text().then(function(text) {
    poemDisplay.textContent = text;
  });
});
```

Style 2:
```javascript
fetch(url).then(function(response) {
  return response.text()
}).then(function(text) {
  poemDisplay.textContent = text;
});
```

In Style 2, each subsequent promise comes after the previous one, rather than being inside the previous one (which can get unwieldly). The only other difference is that we’ve had to include a return statement in front of `response.text()`, to get it to pass its result on to the next link in the chain.