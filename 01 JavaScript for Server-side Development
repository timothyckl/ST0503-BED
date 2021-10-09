## __Table of Contents__

1. [Functions](##Functions)
    - First Class Function
    - Higher-Order Function
    - Closures
2. [JavaScript & Callbacks](##JavaScript-&-Callbacks)
    - Error Handling w/ Callbacks
    - Arrow Functions

## __Functions__

Functions are blocks of organized, reusable code that are used to perform certain processes. 
In JS, functions are first class objects.

#### Structure of a Function 

```js
function myFunc(arg) {
    //code
};
```

Functions accept any number of arguments and also return a value. In the absence of a return statment, a function returns ```undefined```

For example,

```js
function greet(name) {
    console.log(`Hello, ${name}!`);
};
console.log(greet('Joe'));
```
would output:

```js 
Hello, Joe!
undefined
```

#### First Class Functions

What are first class functions?

> Functions are said to be first class when they are treated like any other variable. 
> - Functions that can be passed as arguments to other functions
> - Functions that can be returned by other functions
> -  Functions that can be assigned as a value to a variable

For example,

```js
const anonFunc = function() { //functions without names are anonymous functions
    return 'I am an anonymous function!';
};
console.log(anonFunc());
```

#### Higher Order Functions

What are higher order functions?

> Higher order functions are functions that receive other functions as an argument or returns the functions as output.

For example,

```js
const numArr = [1, 2, 3];
const newArr = numArr.map(function(item) {
    return item * 2;
});

console.log(newArr); // [2, 4, 6]
```

#### Closures

What are closures?

> Closures are a feature in JS which allows the inner function access to variables declared inside the enclosing function. 

Closures follow 3 key properties:

- It has access to variables defined in itself
- It has access to the outer function’s variables
- The inner function will continue to have access to the variables from the outer scope even after the outer function has returned

For example,

```js
function outerFunc() {
  var greeting = 'ayo what the dog doin';
  function innerFunc() {
    console.log('u reached d inner function mabrudda');
    console.log(greeting);
  };
  return innerFunc;
};

var myFunc = outerFunc();
myFunc();
```
outputs:

```js
u reached d inner function mabrudda
ayo what the dog doin
```

## __JavaScript & Callbacks__

By default JS single threaded and run synchronously. This means code is ran in the order they that they are called. Take for example,

```js
function firstFunc() {
    console.log('I am function #1');
};

function secondFunc() {
    console.log('I am function #2');
};

firstFunc(); // firstFunc will execute first
secondFunc(); // secondFunc will execute second
```

### JavaScript

JS was initially created as a browser-only language. Responding to user events, but how would this be possible with a synchronous programming model?

The evironment, aka browser/client provides a set of APIs that support such functionalities, making JS event driven.

Node JS, a runtime environment, utilizes non-blocking I/O operations allowing a single process to serve multiple requests at the same time. This allows for asynchrounous code execution.

See [What is an event loop in JS](https://www.educative.io/edpresso/what-is-an-event-loop-in-javascript)

### Callbacks

Non-blocking I/O operations provide a callback function that is called when the operation is completed.

For example,

```js
function firstFn(){
  // Simulate 2s execution delay
  setTimeout( function(){ // anonymous callback
    console.log('Hello');
  }, 2 * 1000 );
}
function secondFn(){
  console.log('world');	
}

firstFn();
secondFn(); 
```

output:

```js
world
Hello
```

Since ```setTimeout()``` is an asynchrounous function, our code doesn't wait for ```firstFunc()``` 
to respond before executing ```secondFunc()```.

#### Error Handling w/ Callbacks

We can handle errors using callbacks in the event reading data from a file fails. The error object would occupy the first parameter.

```js
function errorHandler(err, data) {
    if (err){ // when err is defined, it returns a truthy value
        console.log(err);
    } else {
        console.log(data);
    }
};

```

#### Arrow Functions

Arrow functions make our code more concise and simplify function scoping. With arrow functions, certain characters/keywords can be omitted.

For example,
```js
// Without arrow function
    function callWife() {
        return 'Make me a sandwich!'
    }

// With arrow function
const callWife = () => 'Make me a sandwich!'
```

Another example w/ previous code:

```js 
const arr1 = [1, 2, 3];
const arr2 = arr1.map(item => item * 2);
console.log(arr2); // [2, 4, 6]
```
