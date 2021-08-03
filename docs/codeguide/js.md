# JavaScript

## Important Concepts & Rules
- `Hoisting` is JavaScript's default behavior of moving declarations to the top.
- Good code explains itself! However, comment what you consider needed - but don’t tell others your life story.

### Functions Functions Functions
- All `Function Declarations` are hoisted.
- A `Function Expression` is an anonymous function that is saved into a variable. They do not get hoisted.
- In a `Regular function`, the `this` keyword is bind to the `window object` instead of the scope of where the function is located.
- In an `Arrow Functions`, the `this` keyword is automatically bind to where the function or class is located.
- Make sure to write smaller, generic helper functions that fulfill one specific task rather than catch-all methods.

### Variable declaration
- Always use strict equality operator `===`. The abstract equality operator `==` only compares value, not type.
- Both `null` and `undefined` represent empty values. When a variable is declared, but not assign a value, JS will automatically set `undefined` as a placeholder.
- If you do `typeOf` `undefined` the value will be `undefined`, whereas the value of `null` will be an object.
- Declare all your variables as a `const` unless the use of `let` is required.
- `let` variables are block scoped.`var` variables are function scoped.
- `let` variables are not added to the global object. `var` variables are added to the global object as properties.
- `let` variables can not be re-declared. It will give you an error. `var` keyword allows you to redeclare a variable without any issue.
- Avoid using `var` to declare variables. `var` variables get 'hoisted', which can lead to unexpected results.
- Avoid confusing undescriptive variable names, for example: `x1 , num21, incrementerForMainLoopWhichSpansFromTenToTwenty`.
- Use shortcut notations to make your code easier to read, for example: `let user = object.username || 'Guest'`, Ternary Operators, and Destructuring.

## Use Strict Mode
- `'use strict';` is a way to opt in to a restricted variant of JavaScript.
- Eliminates some JavaScript silent errors by changing them to throw errors.
- Fixes mistakes that make it difficult for JavaScript engines to perform optimizations.
- [Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) code can sometimes be made to run faster than identical code that's not strict mode.
- Prohibits some syntax likely to be defined in future versions of ECMAScript.

## Useful Array Helpers
- [forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)
- [filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
- [every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- [some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

## Useful Features
### Template Literals (<code>`</code>)
Allows for embedded expressions in a string when enclosed by the backtick character instead of double or single quotes.
```js
const color = 'red';
console.log( `Hello, my favorite color is ${color}!!` );
// Result: Hello, my favorite color is red!!
```

### Spread Operator (`...`)
It takes in an array or object and expands it into individual elements. This operator makes copying and merging arrays a lot simpler.
```js
const fruits = [ 'apple', 'banana', 'kiwi' ];
const basket = [ ...fruits, 'orange', 'strawberries'];
// Result: [ 'apple', 'banana', 'kiwi', 'orange', 'strawberries' ]
```
### Rest Parameters (`...theArgs`)
Allows a function to accept an indefinite number of arguments as an array.
```js
function average( ...theArgs ) {
    const total = theArgs.reduce( (previous, current) => {
        return previous + current;
    });
    return total / theArgs.length;
}
console.log( average( 1, 2, 3, 4, 5 ) );
// Result: 3
```

### Default function parameters
Allows named parameters to be initialized with default values if no value or undefined is passed
```js
function tipCalculator( billAmount, tip = 10 ) {
    return ( tip * billAmount ) / 100;
}
console.log( tipCalculator( 40 ) );
// Result: 4
console.log( tipCalculator( 60, 15 ) );
// Result: 9
```

### Destructuring
Makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
```js
let motorcycle = {
    type: 'Yamaha',
    model: 'R6',
    color: 'Blue',
    name: 'Rosalinda'
}
let { name } = motorcycle;
console.log( name );
// Result: Rosalinda
```

### Optional Chaining
Allows you to access nested object properties without having to verify if the parent property exists every time.
```js
let userAdmin = undefined;
if ( payload.access && payload.access.admin && payload.access.admin[0] ) {
    userAdmin = payload.access.admin[0].user;
}
// With Optional Chaining
const userAdmin = payload.access?.admin?[0]?.user;
```

### Numeric Separators
Mostly a cosmetic change that will help read numeric values easier.
```js
const million = 1_000_000;     // 1000000
const billion = 1_000_000_000; // 1000000000
```

### `Object.fromEntries()`
This method takes a key-value pair and returns a new object whose properties are given by those entries.
```js
const myArray = [ [ 'one', 1 ], [ 'two', 2 ], [ 'three', 3] ];
const obj = Object.fromEntries( myArray );
console.log( obj );
// Result: { one: 1, two: 2, three: 3 }
```
### `Promise`
An object that may produce a single value some time in the future. Either a resolved value, or a reason that it's not resolved. They allow you to defer further actions until after a previous action has completed. This is useful for setting up a sequence of async operations to work correctly.

### `Async/Await functions`
async and await are extensions of promises. Await expressions make promise-returning functions behave as though they're synchronous by suspending execution until the returned promise is fulfilled or rejected.
```js
async function getPostsData() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const posts = await response.json();
        return posts;
    } catch (err) {
        console.error(err);
    }
}
```
## Helpful Resources
- [Free for Dev](https://github.com/ripienaar/free-for-dev)
- [Clean Code JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
- [JavaScript Algorithms and Data Structures](https://github.com/trekhleb/javascript-algorithms)
- [JavaScript Interview Question](https://github.com/sudheerj/javascript-interview-questions)
