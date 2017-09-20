Put JavaScript just before the close of `<body>` if it manipulates DOM. Libraries should be loaded at the bottom unless it is told otherwise.

## String
`indexOf()`: search string
`toLowerCase()`
`toUpperCase()`
`substr()`
`slice()`
`replace()`

`split()`: split into an array
`join()`: array to string

`Number()`: convert to number

## Anonymous functions
Function hidden inside a variable. Not global function.

## Self invoking functions
```javascript
(function(){
	//automatically run when the function is done loading
})();
```
By hiding `function` in itself we do not pollute the enclosing scope. The `()` after the function expression invokes the function immediately. 

## Hoisting
Use variable before it is declared.  
Best practice: declear variables at the top of the scope. 

## Function declarations vs. function expressions
A function declaration is processed when the execution enters the context in which it appears and before any step-by-step code is called (hoisting). Function declarations are only allowed to appear within the program or function body, not in blocks (`{}`).

Function expression is being assessed when it reaches the step-by-step execution of the code and thus we have to declear it before invoking it. 

## Arguments parameter
`arguments` is a collection of all the arguments passed to the function. It has a `length` property. The individual argument values can be obtained by using an array indexing notation. `arguments` is **not** an array. 

Convert `arguments` to an array:

```javascript
var args = Array.prototype.slice.call(arguments);
```

## `this`
**Invocation as a function**: If a function is not invoked as a method, or as a constructor, or through `apply()` or `call()`, then `this` is simply been invoked as a function. With this pattern, this is bound to the global object.

**Invocation as a method**: For methods, `this` is bound to the object on invocation.

**Invocation as a constructor**: Constructor functions get’s declared just like any other functions. To invoke the function as a constructor, we precede the function invocation with the `new` keyword. When this happens, `this` is bound to the new object. For easier distinction, constructor functions are named using **PascalCase** as opposed to camelCase.

## Class

## `const`, `let`, and `var`
`const`: Constant variable, never be reassigned. Scope is in closest `{ }`. Must be immediately assigned with a value. 
`let`: Can reassign value. Scope is in closest `{ }`. Does not support hoisting.
`var`: Can reassign value. Scope is in function. Supports hoisting.

## Arrow functions
In normal function, `this` is bound to the function itself. In arrow founction, `this` is **not** bound to the function.

``` javascript
function name() {
	if (this.name === undefined) {
		this.name = 0;
	}

	this.name++;
}

// arrow function
var functioname = (param1, param2) => {
	console.log(param1 + param2);
	// this is not bound to the function
}

```  

