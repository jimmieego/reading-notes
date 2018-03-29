https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM

Shadow DOM allows hidden DOM trees to be attached to elements in the regular DOM tree — this shadow DOM tree starts with a shadow root, underneath which can be attached any elements you want, in the same way as the normal DOM.

- Shadow host: The regular DOM node that the shadow DOM is attached to.
- Shadow tree: The DOM tree inside the shadow DOM.
- Shadow boundary: the place where the shadow DOM ends, and the regular DOM begins.
- Shadow root: The root node of the shadow tree.

## Basic usage

```javascript
let shadow = elementRef.attachShadow({mode: 'open'});
let shadow = elementRef.attachShadow({mode: 'closed'});

var para = document.createElement('p');
shadow.appendChild(para);

```

`open` means that you can access the shadow DOM using JavaScript written in the main page context. For example: `let myShadowDom = myCustomElem.shadowRoot;`

**Notes**:

- Closed shadow roots are not very useful. Some developers will see closed mode as an artificial security feature. But let's be clear, it's not a security feature. Closed mode simply prevents outside JS from drilling into an element's internal DOM.
- Closed shadow DOM option will prevent axe-core and aXe extensions from being able to look inside the shadow DOM.