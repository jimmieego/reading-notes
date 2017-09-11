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

## Hoisting
Use variable before it is declared.  
Best practice: declear variables at the top of the scope. 