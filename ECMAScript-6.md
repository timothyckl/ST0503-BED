# ECMAScript 6

## let Keyword

```let``` variables are block scoped while ```var``` variables are function scoped.

This means ```let``` variables are scoped to the immediate enclosing block denoted by ```{}``` and ```var``` variables are scoped to immediate function body.

Example:

```js    
function run() {
    {
        var foo = "Foo";
        let bar = "Bar";
        console.log(foo, bar); // Foo Bar
    }

    console.log(foo); // Foo
    console.log(bar); // ReferenceError: bar is not defined
}
```

## const Keyword

```const``` variables do not support assignment and will throw TypeError.

```js    
const name = 'bob';
name = 'da builder';  // TypeError: Assignment to constant variable
console.log(name);
}
```

## Template Literals

Template literals are kept within backticks ``` `` ```, allowing embedded expressions called substitutions. This is useful for string interpolation and multiline strings.

Substitutions are indicated by the dollar sign and curly braces ```${expression}```.

Example:

```js    
const firstName = 'Zhong';
const lastName = 'Xina';

console.log(`Hello, ${firstName} ${lastName}!`);
```

## Searching Strings

```startsWith()```, ```endsWith()``` and ```includes()```   methods return a Boolean value of either ```true``` or ```false```.


```js    
const planet = 'Earth';

console.log(planet.startsWith('Ear')); // true
console.log(planet.endsWith('s')); // false
console.log(planet.includes('h')); // frue
```

```search()``` method returns the __starting index__ of the __first instance__ of the string argument. 

```js    
const planet = 'Earthartartart';
console.log(planet.search('art')); // 1
```

## Symbol Object

A ```symbol``` is a primitive data type that is guaranteed to be unique.

Primitive values while immutable, can be reassigned. For example:

```js    
let x = 1; 
x++; // x has been reassigned
     // but the primitive numeric type has not been mutated
```

A ```symbol``` is a primitive which __cannot__ be recreated. For example:

```js    
const s1 = Symbol();
const s2 = Symbol();

console.log(s1 === s2); // false
```

Symbols allow us to create hidden properties of an object and are used to:
>- Avoid name clashing between properties, since no symbol is equal to another
>- Add properties that the user cannot overwrite, intentionally or without realizing.

For example:

```js    
const id = Symbol();

const courseInfo = {
    title: 'JavaScript',
    topics: ['strings', 'arrays', 'objects'],
    id: 'js-course' // no naming conflict
};

courseInfo[id] = 6969; // adds Symbol() property to object
console.log(courseInfo); // {
                         //     title: 'JavaScript',
                         //     topics: ['strings', 'arrays', 'objects'],
                         //     id: 'js-course',
                         //     Symbol(): 6969
                         // }
```

## Map Object

Similar to objects, maps hold key-value pairs of any type. For example:

```js    
let course = new Map();

course.set('react', {description: 'ui'});
course.set('jest', {description: 'testing'}); 

console.log(course.react); // undefined as dot notation cannot be used with maps
console.log(course.get('react')); // {description: 'ui'}
```

## Sets

\# 

## Array Spread Operator

\# 

## Destructuring Arrays

\# 

## Searching Arrays

\# 

## Object Literal Enhacement

```js    
// before enhancement
function person(name, sound) {
    return {
        name: name,
        sound: sound,
        powerYell: function () {
            let yell = this.sound.toUpperCase();
            console.log(`${yell}! ${yell}!`)
        }
    };
}

// after enhancement
function person(name, sound) {
    return {
        name,
        sound,
        powerYell: function () {
            let yell = this.sound.toUpperCase();
            console.log(`${yell}! ${yell}!`)
        }
    };
}

const p1 = person('Deez', 'ayoo');
console.log(p1.name); // Deez
p1.powerYell(); // AYOO! AYOO!
```
