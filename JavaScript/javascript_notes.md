# JavaScript Notes

<!-- MarkdownTOC -->

- Variables
- Scope
- Closures
  - Controlling side effects with closures
  - Private variables with closures
- Iterables and Iterators
  - User-defined Iterables
- Events
  - Custom Events
- Objects
  - Property attributes
  - Object attributes
  - Inheritance
  - Create object
  - Object properties
- `this`
- Select elements
- Attribute methods
- DOM manipulation
  - Create element
  - Insert element
- Event
- Position
- Promises
- Map, filter and reduce
  - Map
  - Filter
  - Reduce
- Essential Functions
- Regular Expressions

<!-- /MarkdownTOC -->


## Variables
**Variable hoisting**: The JavaScript engine treats all variable declarations using `var` as if they are declared at the top of a functional scope (if declared inside a function) or global scope (if declared outside of a function) regardless of where the actual declaration occurs.

**Block-level declarations**: Block-level declarations are made in block/lexical scopes that are created inside a block “{ }”.
- Use `let` to declare a variable with its scope being only that code block.
- Place `let` declarations at the top in a block so they’ll be available within that entire block.
- Note: If an identifier has already been defined inside a scope, using that same identifier in a `let` declaration inside the same scope throws an error.

Also, no error is thrown if a `let` declaration creates a variable with the same name as that of a variable in it’s outer scope. (This case is same with `const` declarations.)

`const`: The variable can't be reassigned. Every `const` declaration must be initialized at the time of declaration. Its lifecycle is the same as `let`. (Note: properties can be mutated. So for true immutability, use Immutable.js or Mori.)

Accessing a `let` or `const` variables before they’re declared will throw a `ReferenceError`.

## Scope
When a function is defined in another function, the inner function has access to the outer function's variables. This behavior is called **lexical scoping**. However, the outer function does not have access to the inner function's variables. 

## Closures
Whenever you create a function within another function, you have created a **closure**. *The inner function is the closure*. This closure is usually returned so you can use the outer function's variables at a later time.

```javascript
function outerFunction () {
  const outer = `I see the outer variable!`;

  return function innerFunction() {
    console.log(outer);
  }; // return innerFunction
}

outerFunction()(); // I see the outer variable!
```

Since closures have access to the variables in the outer function, they are usually used for two things: 
1. To control side effects
2. To create private variables

### Controlling side effects with closures
When you use closures to control side effects, you're usually concerned with ones that can mess up your code flow like Ajax or timeouts. You create a function that activates the inner closure at your whim.

```javascript
function prepareCake (flavor) {
  return function makeCake (flavor) {
    setTimeout(() => console.log(`Made a ${flavor} cake`), 1000);
  }
}

const makeCakeLater = prepareCake('banana');

// Later in your code ...
makeCakeLater();

```

### Private variables with closures
Variables created in a function cannot be accessed outside the function. Since they can't be accessed, they are also called *private variables*.

```javascript
function secret (secretCode) {
  return {
    saySecretCode () {
      console.log(secretCode);
    }
  };
}

const theSecret = secret('CSS Tricks is amazing');
theSecret.saySecretCode();
```

`saySecretCode` in this example above is the only function (a closure) that exposes the secretCode outside the original secret function. As such, it is also called a *privileged function*.

## Iterables and Iterators
The iterable protocol was introduced to JavaScript in ES2015, and it allows us to define custom iteration behavior on objects so that we can control what values are looped over in a `for...of` loop, which was also introduced in ES2015.

A few built-in objects that implement the iterable protocol include `Array`, `String`, `Map`, `Set` and `NodeList`.

Example:

```javascript
let listItems = document.querySelectorAll('li');

for (let li of listItems) {
  console.log(li.textContent);
}
```

### User-defined Iterables
```javascript
class UserCollection {
  constructor(users) {
    this.users = [].concat(users);
  }

  [Symbol.iterator]() {
    let i = 0;
    let users = this.users;

    return {
      next() {
        if (i < users.length) {
          return { done: false, value: users[i++] };
        }

        return { done: true };
      }
    };
  }
}

let users = new UserCollection([
  { first: 'Yehuda', last: 'Katz' },
  { first: 'Tom', last: 'Dale' },
  { first: 'Taylor', last: 'Otwell' }
]);

for (let user of users) {
  console.log(user);
}
```

You can also use the spread operator to create an array from a sequence of values.

```JavaScript
console.log([...users]);
// [
//   { first: 'Yehuda', last: 'Katz' },
//   { first: 'Tom', last: 'Dale' },
//   { first: 'Taylor', last: 'Otwell' }
// ]
```

## Events

### Custom Events
Use `new CustomEvent()` to create the event, passing in the name of the event. Then use `dispatchEvent()` on the element you want to attach the event to, passing in your new custom event. 

```JavaScript
var makeBlue = function (elem) {

    elem.classList.add('blue');

    // Create a new event
    var event = new CustomEvent('madeBlue');

    // Dispatch the event
    elem.dispatchEvent(event);

};

var elem = document.querySelector('.not-blue');
makeBlue(elem);

// Run function on `madeBlue` event
elem.addEventListener('madeBlue', function (elem) {
    elem.classList.add('color-changed');
}, false);
```

## Objects
Any value in JavaScript that is not a string, a number, `true`, `false`, `null`, or `undefined` is an object. Objects are *mutable* and are manipulated by *reference* rather than by value.

### Property attributes
Properties of objects have associated values called *property attributes*:
- *writable*: whether the value of the property can be set
- *enumerable*: whether the property name is returned by a `for` or `in` loop
- *configurable*: whether the property can be deleted and whether its attributes can be altered

### Object attributes
Every object has three associated *object attributes*:
- *prototype*: reference to another object from which properties are inherited
- *class*: a string that categorizes the type of an object
- *extensible*: flag that specifies (in ES5) whether new properties may be added to the object

The *prototype* attribute of an object creates a chain or linked list from which properties are inherited.

### Inheritance
Inheritance occurs when querying properties but not when setting them is a key feature of JavaScript. It allows us to selectively override inherited properties.   

### Create object
ES5 defines `Object.create()`. First argument is the prototype of the object. Second argument describes the properties of the new object (*property attributes*). This provides the ability to create a new object with an arbitrary prototype.
```javascript
let obj = Object.create({x:1, y:2});
```

### Object properties
We can use square brackets (array notation) to get or set an object's property. Inside the square brackets is a string value which could be dynamic and can change at runtime. The dot notation (.) only works with property identifier which is static and must be hardcoded in the program.
```javascript
let title = book["main title"];
book["main title"] = "ECMAScript";
```

#### Delete properties
The `delete` operator removes a property from an object. The `delete` operator only deletes own properties, not inherited ones.
```javascript
delete book.author;
delete book["main title"];
```
Note: `delete` does not remove properties that have a `configurable` attribute of `false`. Certain properties of the built-in objects are nonconfigurable, as are properties of the global object created by variable declaration and function declaration.

#### Test properties
The `in` operator expects a property name as a string on its left side and an object on its right. It returns `true` if the object has an own property or an inherited property by that name.

It is often sufficient to query the property and use `!==` to make sure it is not `undefined`, but `in` can distinguish between properties that do not exist and properties that exist but have been set to `undefined`.

The `hasOwnProperty()` method of an object tests whether that object has an own property with the given name. It returns `false` for inherited properties.

The `propertyIsEnumerable()` refines the `hasOwnProperty()` test. It returns `true` only if the named property is an own property and its `enumerable` attribute is `true`.

## `this`
http://georgemauer.net/2017/08/03/on-this-in-javascript.html
In JavaScript, `this` is just a function parameter that you don't get to name.

Rules on standard `invocation()`:
- By default this will be the global object (`window` in the browser, `global` in node).
- Unless you are running in strict mode (almost always a good idea) and `use strict` is somewhere in the function's scope chain - then `this` will be undefined.

The dot operator actually modifies the invocation to the right to say that the thing to the left of the dot operator is set as `this`.


## Select elements
- Select an individual element: `getElementById()`, `querySelector()`
- Select multiple elements (nodelists):
    - `getElementsByClassName()`
    - `getElementsByTagName()`
    - `querySelectorAll()`
- Transverse between element nodes: `parentNode`, `previousSibling`, `nextSibling`, `firstChild`, `lastChild`

## Attribute methods
- `getAttribute()`
- `hasAttribute()`
- `setAttribute()`
- `removeAttribute()`
- `className`: get or set the value of the class attribute
- `id`: get or set the value of the id attribute

## DOM manipulation
- `appendChild()`
- `removeChild()`
- `replaceChild()`
- `insertBefore()`
- `createElement()`
- `createTextNode()`

### Create element

Before adding a new element, it needs to be created. `document` acts as a factory for new elements:
- `document.createElement()` used to create elements. 
- `document.createTextNode` used to create text nodes.

### Insert element
#### Insert before an element
The old-school way: You need to call `insertBefore()` on the parent of the element you’re inserting your new element before (the `referenceNode`), and pass in both the new element and the reference node as arguments.

```javascript
// Create a new element
var newNode = document.createElement('div');

// Get the reference node
var referenceNode = document.querySelector('#some-element');

// Insert the new node before the reference node
referenceNode.parentNode.insertBefore(newNode, referenceNode);
```

The ES6 way:
You call the `before()` method on the reference node, and pass in the new node as an argument.

```javascript
// Create a new element
var newNode = document.createElement('div');

// Get the reference node
var referenceNode = document.querySelector('#some-element');

// Insert the new node before the reference node
referenceNode.before(newNode);
```

A polyfill for `before` adds support back to IE9:

```javascript
// from: https://github.com/jserz/js_piece/blob/master/DOM/ChildNode/before()/before().md
(function (arr) {
  arr.forEach(function (item) {
    if (item.hasOwnProperty('before')) {
      return;
    }
    Object.defineProperty(item, 'before', {
      configurable: true,
      enumerable: true,
      writable: true,
      value: function before() {
        var argArr = Array.prototype.slice.call(arguments),
          docFrag = document.createDocumentFragment();

        argArr.forEach(function (argItem) {
          var isNode = argItem instanceof Node;
          docFrag.appendChild(isNode ? argItem : document.createTextNode(String(argItem)));
        });

        this.parentNode.insertBefore(docFrag, this);
      }
    });
  });
})([Element.prototype, CharacterData.prototype, DocumentType.prototype]);
```

#### Insert after an element
Old way:

```javascript
// Create a new element
var newNode = document.createElement('div');

// Get the reference node
var referenceNode = document.querySelector('#some-element');

// Insert the new node before the reference node
referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling);
```

Modern approach:

```javascript
// Create a new element
var newNode = document.createElement('div');

// Get the reference node
var referenceNode = document.querySelector('#some-element');

// Insert the new node before the reference node
referenceNode.after(newNode);
```

Polyfill supporting back to IE9:

```javascript
//from: https://github.com/jserz/js_piece/blob/master/DOM/ChildNode/after()/after().md
(function (arr) {
  arr.forEach(function (item) {
    if (item.hasOwnProperty('after')) {
      return;
    }
    Object.defineProperty(item, 'after', {
      configurable: true,
      enumerable: true,
      writable: true,
      value: function after() {
        var argArr = Array.prototype.slice.call(arguments),
          docFrag = document.createDocumentFragment();

        argArr.forEach(function (argItem) {
          var isNode = argItem instanceof Node;
          docFrag.appendChild(isNode ? argItem : document.createTextNode(String(argItem)));
        });

        this.parentNode.insertBefore(docFrag, this.nextSibling);
      }
    });
  });
})([Element.prototype, CharacterData.prototype, DocumentType.prototype]);

```


## Event
- Event target is the originator of the event, not necessarily the element the handler was added to.
- Element the handler was added to is referred to as the "current target" by the W3C
  - Acessible via `e.currentTarget` or `this`
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

## Position
- `screenX` and `screenY` indicate the position of the cursor within the entire screen on the monitor, measuring from the top left corner of the screen (rather than the browser).
- `pageX` and `pageY` indicate the position of the cursor within the entire page. The top of the page may be outside of the viewport so even if the cursor is in the same position, page and client coordinates can be different.
- `clientX` and `clientY` indicate the position of the cursor within the browser’s viewport. If the user has scrolled down and the top of the page is no longer in view, it will not affect the client coordinates.

## Promises
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




## Map, filter and reduce
- If I already have an array and I want to do the exact same **operation** on each of the elements in the array and return the same amount of items in the array, use the `map`.
- If I already have an array, but I only want to have items in the array that match certain criteria, use `filter`.
- If I already have an array, but I want to use the values in that array to **create** something completely new, use `reduce`.

Advantages:
- Avoid mutating an array inside a `forEach` or `for` loop.
- Assign its result directly to a new variable, rather than push into an array defined eleswhere.

### Map
Defined on `Array.prototype`. Can call it on any array. It accepts a callback as its first argument. It executes that callback on every element within the array, returning a *new* array with all of the values that the callback returned.

```javascript
const animals = [
    {
        "name": "cat",
        "size": "small",
        "weight": 5
    },
    {
        "name": "dog",
        "size": "small",
        "weight": 10
    },
    {
        "name": "lion",
        "size": "medium",
        "weight": 150
    },
    {
        "name": "elephant",
        "size": "big",
        "weight": 5000
    }
]

let animal_names = animals.map((animal, index, animals) => {
    return animal.name
})

//another version
let animal_names = animals.map(function (animal, index, animals) {
    return animal.name;
});

//ES6
let animal_names = animals.map((animal) => animal.name );
```

`map` accepts three values in the callback function, namely:
- The current item of the array
- The current index of the current item
- The entire array

Implementation of `map`:
```javascript
var map = function (array, callback) {

    var new_array = [];

    array.forEach(function (element, index, array) {
       new_array.push(callback(element));
    });

    return new_array;

};
```

### Filter
Defined on `Array.prototype`. Pass it a callback as its first argument. `filter` executes the callback on each element of the array, and return a new array containing only the elements for which the callback returned `true`.

```javascript
let small_animals = animals.filter((animal) => {
    return animal.size === "small"
})

//ES6
let small_animals = animals.filter((animal => animal.size === "small"));
```
The `filter` operator accepts the same parameters (current item, index and entire array) in the callback function. Need to make sure that the `return` returns a boolean value.

Implementation:

```javascript
var filter = function (array, callback) {

    var filtered_array = [];

    array.forEach(function (element, index, array) {
        if (callback(element, index, array)) {
            filtered_array.push(element);    
        }
    });

    return filtered_array;

};
```

### Reduce
`reduce` takes all of the elements in an array and reduces them into a **single** value. First argument is the callback. Second, optional argument is the value to start combining all array elements into.

```javascript
let total_weight = animals.reduce((weight, animal, index, animals) => {
    return weight += animal.weight
}, 0)

//ES6
let total_weight = animals.reduce((weight, animal) => weight + animal.weight );
```
- The first parameter is the total-so-far, or accumulated value.
- The second parameter is the current item in the array.
- The third parameter is the current index.
- The last parameter is the full array.

```javascript
var total = [1, 2, 3, 4, 5].reduce(function (previous, current) {
    return previous + current;
}, 0); // The second argument of reduce, 0, is the previous value for the first iteration.
```
The callback gets a previous value on each iteration. On the first iteration, there is no previous value. You have the option to pass `reduce` an initial value. It acts as the "previous value" for the first iteration.

It returns the end value of the first parameter at the end of each `reduce` function.

Implementation:
```javascript
var reduce = function (array, callback, initial) {
    var accumulator = initial || 0;

    array.forEach(function (element) {
       accumulator = callback(accumulator, element);
    });

    return accumulator;
};
```

## Essential Functions
- [debounce](https://gist.github.com/jimmieego/121b00f8276e1cf4f2ee13359465cf61)


## Regular Expressions
Regular expressions are represented with RegExp objects and can be created with literal syntax or with RegExp constructor. Expressions can be modified with attributes:
- `g` performs a global match
- `i` performs case-insensitive matching
- `m` enables multiline mode
