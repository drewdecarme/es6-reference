# ECMA2015 (ES6) Quick Reference Guide
This guide is designed to be a resource that outlines all of the major concepts of ES6 in a brief and concise manner. The concepts and some examples were taken from Nicholas C. Zakas' book "Understanding ECMAScript 6: The Definiitive Guide for Javscript Developers".

# Table of Contents
  - [Block Bindings](#block-bindings)
    - [Block Scopes](#block-scopes-lexical-scopes)
    - [Declarations](#declarations)
    - Functions in Loops
  - Regular Expressions
    - Unicode Support
      - codepointAt()
      - normalize()
      - u flag
      - y flag
  - [Strings](#strings)
    - [Substrings](#substrings)
    - [Template Literals](#template-literals)
    - Tags
  - [Functions](#functions)


## Block Bindings
### Block Scopes (Lexical Scopes)
  - can be placed inside of a function or inside of a block
  - mimicks the same uniforimity as in c-based languages

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

### Temporal Dead Zone
A variable declared with `let` or `const` cannot be access until after the declaration. A variable declared with `var` **can** due to the fact that is is _hoisted_ to the top of its function level definition.
```js
console.log(typeof value);  // "undefined"
if (condition) { let value = 'blue' };
```

### Functions in Loops (TBD)



## Regular Expressions



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
`.strstartsWith(sbstr)` returns `true` if the given text is found at the beginning of the string
```js
let msg = `bookkeeper`;
console.log(msg.includes('book'))     // true
console.log(msg.includes('keeper'))   // false
```

#### `endsWith()`
`str.endsWith(sbstr)` returns `true` if the given text is found at the end of the string
```js
let msg = `bookkeeper`;
console.log(msg.includes('keeper'))   // true
console.log(msg.includes('book'))     // false
```

#### ES5 Translated Concepts
`str.indexOf(sbstr)` & `str.lastIndexOf(sbstr)` should be used to find the position of a substring within the string
`indexOf()` and `lastIndexOf()` can be used with regular expressions
`includes()`, `startsWith()`, and `endsWith()` **cannot** be used with regular expressions


### Template Literals
#### General
Defined by using back ticks instead of a double or single quote
```js
let message = `This is the message`;
let otherMessage = `This is the message`;

console.log(message === otherMessage) // true
```
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
An expression can be included by enclosing it in `${}`
```js
let name = 'Drew'
const welcome = `Welcome to the team, ${name}!`;
console.log(welcome)  // Welcome to the team, Drew!;
```
#### Tags
A _template tag_ performs a transformation on the template literal and returns the final string value
**Example TBD**



## Functions
### Default Parameters
### Rest Parameters
### Spread Operator
### Name
### Block Level Functions
### Arrow Functions
### Tail Call Optimization






  





