# JavaScript Notes

<!-- MarkdownTOC -->

- Variables
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
- Event
- Position
- Promises
- ES6 Functions
  - Default parameters in ES6
  - Rest Parameters
  - Arrow Functions
- ES6 classes, inheritance, and static members
- ES6 arrays
  - Array.from
  - Array.of
  - Array.keys, Array.values, Array.entries
  - Array.find
  - Array.findIndex
  - Array.fill
  - Array.copyWithin
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

Before adding a new element, it needs to be created. `document` acts as a factory for new elements:
- `document.createElement` used to create elements. ``
- `document.createTextNode` used to create text nodes.

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

## ES6 Functions
### Default parameters in ES6
```javascript
function counts(number1 = 5, number2 = 10) {
  // do anything here
}
```

NOTE: When a value of `undefined` is passed for a parameter with default argument, as expected the value passed is **invalid** and the **default parameter value is assigned**. But if `null` is passed, it is considered **valid** and the **default parameter is not used** and `null` is assigned to that parameter.

### Rest Parameters
A rest parameter is simply a named parameter which is preceded by three dots(…). This named parameter becomes an **array** which contains rest of the parameters(i.e apart from the named parameters) passed during function call.

There can only be one rest parameter, and it has to be the last parameter.

Example:
```javascript
function pickProperties(object, ...properties) {
  let result = {};

  for (let i = 0, len = properties.length; i < len; i++) {
    result[properties[i]] = object[properties[i]];
  }
  return result;
}
let vehicle = {
  typeOfVehicle: 'car',
  name: 'VANTAGE',
  maker: 'Aston Martin',
  color: 'grey'
};
let vehicleData = pickProperties(vehicle, 'typeOfVehicle', 'maker', 'color');
console.log(vehicleData.typeOfVehicle); // "car"
console.log(vehicleData.maker); // "Aston Martin"
```

### Arrow Functions
Arrow functions begin with the **arguments**, followed by the **arrow** (=>), followed by the **function body**.

```javascript
let add = (no1, no2) => no1 + no2;
// equivalent to:
let add = function(no1, no2) {
  return no1 + no2;
};
```

If there are no arguments at all, you must include empty parentheses like below:
```javascript
let getMessage = () => 'Hello World';
// equivalent to:
let getMessage = function() {
  return 'Hello World';
}
```

For a function body with just a return statement, curly braces are **optional**. For a function body having more than just a return statement, you need to wrap the body in curly braces just like traditional functions. Example:
```javascript
let calculate = (no1, no2, operation) => {
    let result;
    switch (operation) {
        case 'add':
            result = no1 + no2;
            break;
        case 'subtract':
            result = no1 - no2;
            break;
    }
    return result;
};
```

Another example:
```javascript
// with arrow function
let result = sampleArray.filter(element => element > 5000);
// without arrow function
let result = sampleArray.filter(function(element) {
  return element > 5000;
});
```

Notes:
- Arrow functions can’t be called with new, can’t be used as constructors (and therefore lack prototype as well).
- Arrow functions have their own scope, but there’s no ‘this’ of their own.
- No arguments object is available. You **can use** rest parameters however.

## ES6 classes, inheritance, and static members
**Define a class**:
```javascript
class Profile {
    constructor(name) {
        console.log('User ${name} was created.');
        this.name = name;
    }
}

// How to instantiate the class
const user = new MyClass('Aram'); // logs: "User Aram was created"
```

Note a class constructor cannot be made static in JavaScript via the `static` keyword, but you can make class members as static using the keyword.

**Class inheritance**:
- Methods defined on the base are accessible in the child class.
- If the child class declares its own constructor then it must invoke the parents constructor via `super()` before it can access `this`.

```javascript
class Car {
    constructor() {
        this.logger = console.log;
    }
    log() {
        this.logger(`Hello ${this.name}`);
    }
}

class SuvCar extends Car {
    constructor() {
        super();
        this.name = 'SUV Car Name';
    }
}

// Usage sample
const suvCar = new SuvCar();
suvCar.log(); // logs: "Hello SUV Car Name"
```

**Static methods and properties**:
Static methods and properties are defined on the *class/constructor itself*, not on instance objects. These are specified in a class definition by using the `static` keyword.

```javascript
class MyClass {
    static myStaticMethod() {
        return 'Hello';
    }

    static get myStaticProperty() {
        return 'Goodbye';
    }
}

// samle usage of static methods
console.log(MyClass.myStaticMethod()); // logs: "Hello"
console.log(MyClass.myStaticProperty); // logs: "Goodbye"

// just like you expect, Static properties are not defined on object instances:

const myClassInstance = new MyClass();
console.log(myClassInstance.myStaticProperty); // logs: undefined

//However, they are defined on subclasses:
class MySubClass extends MyClass {};

console.log(MySubClass.myStaticMethod()); // logs: "Hello"
console.log(MySubClass.myStaticProperty); // logs: "Goodbye"
```

JavaScript classes are just wrappers around JavaScript’s already existing [prototype-based inheritance](http://www.w3schools.com/js/js_object_prototypes.asp).

## ES6 arrays
### Array.from
`Array.from`: create arrays from other types of collections
Select a group of DOM nodes:
```javascript
Array.from(document.querySelectorAll('*'))  // returns Array
```

`Array.from` can also be used instead of `Array.map` to map elements.
```javascript
Array.from(document.querySelectorAll(‘*’), console.log)
```

Use `Array.from` to populate new Arrays:
```javascript
Array.from(new Array(5), k=>'val')
// ['val','val','val','val','val']
```

### Array.of
Can be used as an alternative to the Array constructor, and when passed a single number, will create that value as an element in the array, instead of creating that number of elements — which is what the Array constructor does.
```javascript
Array.of(5)
\\[5]
Array.of(5, 6)
\\[5, 6]
new Array(5)
\\ [undefined x 5]
```

### Array.keys, Array.values, Array.entries
Return iterators for the keys, values, and entries of an array, respectively. `.next()` can be called to advance the array.

### Array.find
Takes a function to find an element in the array, and returns undefined if it does not exist.
```javascript
['a', 'b', 'c'].find(k => k=='b')
\\ 'b'
```

### Array.findIndex
Works similarly to `Array.find`, and returns the index where the element was found, or `-1`.

### Array.fill
Fills an array with a value, with optional start and end indexes. Has the signature `Array.fill(value, start, end)`

### Array.copyWithin
Copy blocks of elements to other parts of the array. Has the signature `Array.copyWithin(target, start, end)`. The target is the element index to be copied over. Start and end are optional, and are the elements to be copied.
```javascript
[1, 2, 3, 4, 5, 6, 7, 8].copyWithin(2, 5)
\\ The third element (target index=2) will be copied over with the values starting at element index 5.
\\ [ 1, 2, 6, 7, 8, 6, 7, 8]

[1, 2, 3, 4, 5, 6, 7, 8].copyWithin(2, 5, 6)
\\ An end value of 6 means only one element (index 5–6) is copied over.
\\ [1, 2, 6, 4, 5, 6, 7, 8]
```


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
