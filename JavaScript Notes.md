# JavaScript Notes

## Variables
**Variable hoisting**: The JavaScript engine treats all variable declarations using `var` as if they are declared at the top of a functional scope (if declared inside a function) or global scope (if declared outside of a function) regardless of where the actual declaration occurs.

**Block-level declarations**: Block-level declarations are made in block/lexical scopes that are created inside a block “{ }”. 
- Use `let` to declare a variable with its scope being only that code block.
- Place `let` declarations at the top in a block so they’ll be available within that entire block.
- Note: If an identifier has already been defined inside a scope, using that same identifier in a `let` declaration inside the same scope throws an error.
Also, no error is thrown if a `let` declaration creates a variable with the same name as that of a variable in it’s outer scope. (This case is same with `const` declarations.)

`const`: The variable can't be reassigned. Every `const` declaration must be initialized at the time of declaration. Its lifecycle is the same as `let`. (Note: properties can be mutated. So for true immutability, use Immutable.js or Mori.)

Accessing a `let` or `const` variables before they’re declared will throw a `ReferenceError`.

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
`appendChild()`
`removeChild()`
`replaceChild()`
`insertBefore()`
`createElement()`
`createTextNode()`

## Event
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
