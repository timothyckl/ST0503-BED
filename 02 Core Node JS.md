02 Core Node JS

## Table of Contents

1. [Nodejs File-Based Module System](##)
    - module.exports
    - require()
2. [Modules, Callbacks and Error Handling](##) 


## Nodejs File-Based Module System

- Each file is its own module
- Current modules are exported with module.exports
- To import a module, use the require function

### module.exports

By using exports.module, we are able to export the function. 

Syntax:

```js    
// formula.js
multiplyFunct = (x, y) => x * y;

module.exports=multiplyFunct

// main.js
const mulFn = require('./formula');

console.log(mulFn(2,3));
```

If we need to export multiple functions:

```js
// formula.js
multiplyFunct = (x, y) => x * y;
addFunct = (x, y) => x + y;

module.exports.mulFn=multiplyFunct;
module.exports.addFn=addFunct;

// main.js
const formula = require('./formula');

console.log(“Multiply 2 x 3=”+formula.mulFn(2,3));
console.log(“Add 2 + 3=”+formula.addFn(2,3));
```

If we have multiple functions, it is best to declare them in an object and export:
```js    
// formula.js
module.exports = {
    mulFn: (x, y) => x * y,
    addFn: (x, y) => x + y
};

// main.js
const formula = require('./formula');

console.log(formula.mulFn(2, 3))
console.log(formula.addFn(2, 3))
```

### require()

When importing a module with require(), Node runs the destination JS file in a new scope and returns what was the final value for module.exports in that file.

> __Note:__ module.exports is already defined to be a new empty object in every file. That is, module.exports = {} is implicitly present. By default, every module exports an empty object, in other words, {}.

## Modules, Callbacks and Error Handling

We can combine concepts of modules, callbacks and error handling in node js modules

Assuming the multiply function contains a “complex” I/O asynchronous operation requiring much time and also we do not allow any “infinity” input values for the function arguments, and any attempt to pass in “infinity” values should return an error to the caller. 

```js    
// formula.js
module.exports = {
    mulFn: (x, y, callback) => {
        if ((x || y) == Infinity) {
            setTimeout(() => {
                callback(new Error('Input values cannot be infinity!'),
                    null);
            }, 2000);
        } else {
            setTimeout(() => {
                callback(null, x * y);
            }, 2000);
        }
    },
    addFn: (x, y, callback) => {
        if ((x || y) == Infinity) {
            setTimeout(() => {
                callback(new Error('Input values cannot be infinity!'),
                    null);
            }, 2000);
        } else {
            setTimeout(() => {
                callback(null, x + y);
            }, 2000);
        }
    }
}

// main.js
const formula = require('./formula')

const errorHandler = (err, data) => {
    if (err) {
        console.log(err.message);
    } else {
        console.log(data);
    }
};

formula.mulFn(2, 3, errorHandler);
formula.mulFn(Infinity, 3, errorHandler); # logs error message 
```
