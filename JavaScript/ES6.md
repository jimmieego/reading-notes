<!-- MarkdownTOC -->

- ES6 Functions
  - Default parameters in ES6
  - Rest Parameters
  - Arrow Functions
- ES6 classes, inheritance, and static members
  - Class inheritance
  - Static methods and properties
- ES6 arrays
  - Array.from
  - Array.of
  - Array.keys, Array.values, Array.entries
  - Array.find
  - Array.findIndex
  - Array.fill
  - Array.copyWithin

<!-- /MarkdownTOC -->


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

    methodOne() {
      //
    }

    static methodTwo() {
      //
    }
}

// How to instantiate the class
const user = new MyClass('Aram'); // logs: "User Aram was created"
```

If a class's constructor has too many parameters, consider using an object as the parameter. 

Note a class constructor cannot be made static in JavaScript via the `static` keyword, but you can make class members as `static` using the keyword. A static method is a property of the class, not the object. A static method could be used as a helper method for objects.

For organization, a class can be stored as a module. A module is just a file that contains your code. To make a class into a module, we add an `export` statement before it. 

```javascript
export class Profile { 
  //
}
```

To use the Profile class in another file, we import it.

```javascript
import { Profile } from Profile
```

Where the `{ }` contains the values that were exported from the module, and `from Profile` is a reference to the file Profile.js.

### Class inheritance
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

### Static methods and properties
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