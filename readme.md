# ECMA2015 (ES6) Quick Reference Guide
This guide is designed to be a resource that outlines all of the major concepts of ES6 in a brief and concise manner. The concepts and some examples were taken from Nicholas C. Zakas' book "Understanding ECMAScript 6: The Definiitive Guide for Javscript Developers".

# Table of Contents
  - [Block Bindings](#block-bindings)
    + [Block Scopes](#block-scopes-lexical-scopes)
    + [Declarations](#declarations)
    + Functions in Loops
  - Regular Expressions
  - [Strings](#strings)
    + [Substrings](#identifying-substrings)
    + [Template Literals](#template-literals)
    + Tags
  - [Functions](#functions)
    + [Default Parameters](#default-parameters)
    + [Rest Parameters](#rest-parameters)
    + [Spread Operator](#spread-operator)
    + Name
    + Block Level Functions
    + [Arrow Functions](#arrow-functions)
    + Tail Call Optimization
  - Objects
    + Literal Syntax
    + Methods
    + Prototype



## Block Bindings
### Block Scopes (Lexical Scopes)
  - can be placed inside of a function or inside of a block
  - mimics the same uniformity as in c-based languages

### Declarations
#### `var`
`var` is always hoisted outside of its block scope and to its higher level function declaration
```js
var otherStuff = 'things'

function stuff(otherStuff) {
  if(otherStuff === 'things'){
    var moreStuff = 'more things';
  }
  return this;
}
```
... is actually ...
```js
var otherStuff = 'things';

function stuff(otherStuff) {
  var moreStuff = 'more things';

  if(otherStuff === 'things'){
  }
  return this;
}

console.log(window.otherStuff)  // "things"
```

#### `let`
`let` essentially replaces `var` except for the fact that unlike `var`, `let` isn't hoisted to the top of the function declaration; it remains defined in its block level. Note that any variable cannot be redefined once it is already defined.
```js
var car = 'ford';
let car = 'jeep'; // error
```

#### `const`
Once the binding is defined, the binding cannot be changed. In addition to the singular value, `const` must be initialized on declaration.
```javascript
const item = 30;    // valid
item = 50;          // invalid
item = () => '50';  // invalid
const item;         // invalid
```
If the value that is bound is an _object_, the value **can** be changed. The declaration prevents the modification of the binding, not the value. The constant cannot be rebound to another binding.
```js
const guy = { name: 'drew' };
guy.name = 'steve';       // valid
guy = { name: 'steve' }   // invalid
guy = 'drew';             // invalid
guy = () => 'drew';       // invalid
```
#### Similarities
`const` and `let` are block level declarations and cannot be accessed outside of the block scope level scope they are defined in
```js
function doStuff(){
  let things = 'things'
  if (typeof things === 'string') {
    console.log(things);  // "undefined"
  }
  console.log(things);  // "things"
}
```
If you use `let` and `const` in the global scope, a new binding is created in the global scope but **no property is added** to the global object
```js
var house = 'brick';
let car = 'ford';
console.log(window.house) // "brick"
console.log(window.car)   // "undefined"
```

#### Temporal Dead Zone
A variable declared with `let` or `const` cannot be accessed until after the declaration. A variable declared with `var` **can** due to the fact that is is _hoisted_ to the top of its function level definition.
```js
console.log(typeof value);  // "undefined"
if (condition) { let value = 'blue' };
```
### Functions in Loops (TBD)



## Regular Expressions (TBD)



## Strings
### Identifying Substrings
#### `includes()`
`str.includes(sbstr)` returns `true` if the given text is found anywhere within the string
```js
let msg = `bookkeeper`;
console.log(msg.includes('keep'))   // true
console.log(msg.includes('keeps'))  // false
```

#### `startsWith()`
`.str.startsWith(sbstr)` returns `true` if the given text is found at the beginning of the string
```js
let msg = `bookkeeper`;
console.log(msg.startsWith('book'))     // true
console.log(msg.startsWith('keeper'))   // false
```

#### `endsWith()`
`str.endsWith(sbstr)` returns `true` if the given text is found at the end of the string
```js
let msg = `bookkeeper`;
console.log(msg.endsWith('keeper'))   // true
console.log(msg.endsWith('book'))     // false
```

#### ES5 Translated Concepts
  - `str.indexOf(sbstr)` & `str.lastIndexOf(sbstr)` should be used to find the position of a substring within the string and **can** be used with regular expressions
  - `includes()`, `startsWith()`, and `endsWith()` **cannot** be used with regular expressions



### Template Literals
#### Simple Literal
Defined by using back ticks instead of a double or single quote
```js
let message = `This is the message`;
let otherMessage = `This is the message`;

console.log(message === otherMessage) // true
```

#### Multi-line Literal
Supports multi-line string concatenation. White space, spaces, and tabs are all parsed and will output based upon what is tabbed.
```js
const hw = `hello
world`;
console.log(hw);  
// "hello
// world"

const hw2 = `hello
    world`;
console.log(hw2);
// "hello
//    world"
```

#### Substitutions
An expression can be included by enclosing it in `${}`
```js
let name = 'Drew'
const welcome = `Welcome to the team, ${name}!`;
console.log(welcome)  // Welcome to the team, Drew!;
```

#### Tags
A _template tag_ performs a transformation on the template literal and returns the final string value
**Example TBD**

#### Raw Values



## Functions
### Default Parameters
Define default values by using an `=` sign.
```js
function getValue() {
  return 5;
}
function request(url, timeout = 2000, callback = getValue()) {
  console.log(callback());  // 5
}
```

#### Previous for Later
Use a previous parameter as the default for a later parameter
```js
function add(first, second = first){
  return first + second
}
console.log(add(1, 1))  // 2
console.log(add(1))     // 2
```

#### Previous for Later Functional Parameter
Use a previous parameter as the parameter for a later functional parameter
```js
function getValue(value) {
  return value + 5;
}
function add(first, second = getValue(first)) {
  return first + second;
}
console.log(add(1, 1))  // 2
console.log(add(1))     // 7
```
#### Exceptions
You cannot use a later parameter as the default for a previous parameter
```js
function add(first = second, second) {
  // second hasn't been declared yet, so first cannot use it
}
```

### Rest Parameters
If there is an unknown amount of parameters passed into a function, using three dots followed by a string `...stuff` will throw all of those unnamed parameters into an array. There can only be 1 rest parameter and it has to be the _last_ parameter
```js
function doSomething(first, second, third, ...rest){
  console.log(typeof rest === 'object');    // true
  console.log(rest[1]);                     // 5
}
doSomething(1, 2, 3, 4, 5, 6, 7);
```


### Spread Operator
Allows you to specify an array that should be split and passed in as separate arguments to a function
```js
let values = [25, 50, 75, 100];
// ES5
console.log(Math.max.apply(Math, values));  // 100
// ES6
console.log(Math.max(...values));           // 100
```

### Name
### Target
### Block Level Functions
Block level functions declared without `let` act like `var` declarations in that they are hoisted to the top of their block definition. Block level functions declared using `let` or `const` remain in their block and aren't hoisted.
```js
if (true) {
  console.log(doSomething());           // "I did it!"
  console.log(typeof doSomethingElse);  // throws an error

  function doSomething() {
    return 'I did it!';
  }

  let doSomethingElse = function() {
    return 'Huh?'
  }

  console.log(doSomething());           // "I did it!"
  console.log(typeof doSomethingElse);  // "function"
}
```
### Arrow Functions
Simply put, they're just functions declared using a fat arrow `=>`. They're appropriate to use anywhere you're currently using an anonymous function expression, such as with callbacks.

#### 1 argument
```js
let reflect = value => value;
// ... is the same as
let refelct = function(value) {
  return value;
};
```

#### 2 arguments
```js
let add = (one, two) => one + two;
// ... is the same as
let add = function(one, two) {
  return one + two;
};
```

#### No arguments
```js
let getStuff = () => 'the stuff';
// ... is the same as
function getStuff() {
  return 'the stuff';
};
```

#### More than just a return statement
```js
let calc = (a, b, c, ...d) => {
  let u = a + b;
  let late = c + d[2];
  return u + late;
};
// ... is the same as
function calc = (a, b, c, d, e, f) {
  let u = a + b;
  let late = c + f;
  return u + late;
};
```

#### Return an Object
```js
let getItem = id => ({ id: id, name: "temp" });
// ... is the same as
let getItem = function (id) {
  return {
    id: id,
    name: "Temp"
  };
};
```

#### Immediately Invoke
Wrap the arrow function in parentheses
```js
let person = (name => {
  return {
    getName: function() {
      return name;
    }
  }
})('Drew');
console.log(person.getName());  // "Drew"
```

#### Array Processing
```js
let values = [1, 45, 3, 5, 7, 10];
let sorted = values.sort((a, b) => a - b);
console.log(sorted);  // [1, 3, 5, 7, 10, 45]
```

#### Notable Differences from `function()`
  - No `this`, `arguments`, and `new.target` bindings
  - Cannot be called with `new`
  - No `prototype`
  - Cannot change `this`
  - No `arguments` object
  - No duplicate named parameters
  - Possess the `name` property

#### No `new`
Arrow functions are designed to be throwaway functions and cannot be used to define new types
```js
var type = () => {};
let object = new type() // error!
```

#### No `this`
The value of `this` inside an arrow function can only be determined by looking up the scope chain.
  - If the arrow function is contained within a non-arrow function, `this` will be the same as the containing function.
  - If the arrow function is contained within an arrow function, `this` refers to the contained arrow function
  - If the arrow function is contained outside of a non-arrow function, `this` refers to the global scope
```js
let stuff = {
  id: '99128dfasdf',
  init() {
    document
      .addEventListener('click', event => this.doSomething(event.type), false);
      // this refers to the this in stuff.id
  },
  doSomething(type) {
    console.log(`Yoooo ${type} for ${this.id}`);
  }
}
```



### Tail Call Optimization

## Objects
### Literal Syntax
#### Property Initializer
#### Concise Methods
**Formal Method Definition**
#### Computed Property Names

### Methods
#### `Object.is()`
#### `Object.assign()`
#### Duplicate Object Literal Keys
#### Enumeration

### Prototype
#### Changing an Objects Prototype
#### Super






  





