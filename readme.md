# ECMA2015 (ES6) Quick Reference Guide
This guide is designed to be a resource that outlines all of the major concepts of ES6 in a brief and concise manner. The concepts and some examples were taken from Nicholas C. Zakas' book "Understanding ECMAScript 6: The Definiitive Guide for Javscript Developers".

Examples below will contain the following:
  1. Title of the Concept
  2. 
  2. Breakdown of the Concept
  3. Examples of the Concept


# Table of Contents
  - [Block Bindings](#block-bindings)
    - [Block Scopes](#block-scopes)
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
  - if `var` is defined inside of a block scope is hoisted to the top of the block
  - if `var` is defined outside of a block scope, it is hoisted to the global scope

#### `let`
**Difference between `var` and `let`
  - `let` unlike `var` is not hoisted to the top of a funciton declaration
  - replace `var` with `let` to declare a variable but limit the variables scope to only the current code block
  - cannot redefine an already defined variable inside of a block scope

#### `const`
  - once defined, values cannot change
  - must be initalized on declaration
```js
const item = 30;  // valid
const item;       // invalid
```
  - if the value is an object, the value **can** be changed. 
  - declaration prevents the modification of the binding, not the value
```js
const guy = { name: 'drew' };
guy.name = 'steve';       // valid
guy = { name: 'steve' }   // invalid
```
#### Similarities
  - `const` and `let` are block level declarations and cannot be accessed outside of the block scope level scope they are defined in
  - if you use `var` in the global scope, a new variable is added to the global object `window` in browsers
  - if you use `let` and `const` in the global scope, a new binding is created in the global scope but **no property is added** to the global object

#### Temporal Dead Zone
  - cannot access a `let` or `const` declaration before is declaration due to the fact that it doesn't hoist
```js
console.log(typeof value);  // "undefined"
if (condition) { let value = 'blue' };
```

### Functions in Loops (TBD)



## Regular Expressions



## Strings
#### Substrings
  - `string.includes(substring)` returns `true` if the given text is found anywhere within the string
  - `string.startsWith(substring)` returns `true` if the given text is found at the beginning of the string
  - `string.endsWith(substring)` returns `true` if the given text is found at the end of the string
  - `string.indexOf(substring)` & `string.lastIndexOf(substring)` should be used to find the position of a substring within the string
  - `indexOf()` and `lastIndexOf()` can be used with regular expressions
  - `includes()`, `startsWith()`, and `endsWith()` **cannot** be used with regular expressions

#### Template Literals
  - act like regular strings delimited by backticks (`) instead of double or single quotes
  - to use a backtick in a string, escape it with a `\`
  - multi-line template literals require no special syntax; just type a next line. However, all white space is a part of the string so watch out for the indentation
```js
const hw = `hello
world`;

console.log(hw);  //"hello
world"
```
  - an expression, variable, string, etc... can all be substitued inside of a template literal by enclosing it in `${jsExpression() || string || var || etc... }`;
  - tags (TBD)



## Functions
### Default Parameters
### Rest Parameters
### Spread Operator
### Name
### Block Level Functions
### Arrow Functions
### Tail Call Optimization






  





