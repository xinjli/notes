# 0x344 JavaScript

- [1. Foundation](#1-foundation)
    - [1.1. Lexical Structure](#11-lexical-structure)
- [2. Type, Value and Variables](#2-type-value-and-variables)
    - [2.1. Variable Declarations](#21-variable-declarations)
        - [2.1.1. var](#211-var)
        - [2.1.2. let, const](#212-let-const)
    - [2.2. Primitive Types](#22-primitive-types)
        - [2.2.1. Number](#221-number)
        - [2.2.2. String](#222-string)
        - [2.2.3. Boolean](#223-boolean)
    - [2.3. Object Types](#23-object-types)
        - [2.3.1. Object](#231-object)
            - [Global Object](#global-object)
        - [2.3.2. Array](#232-array)
- [3. Concurrent Model](#3-concurrent-model)
- [4. Reference](#4-reference)

## 1. Foundation
### 1.1. Lexical Structure
Several rules about lexical structures in javascript

- javascript is case-sensitive
- identifier must start with letter, underscore or dollar sign
- unicode can be used in javascript
- Semicolon is used to separate statement, but can be omitted with a line break. The general rule is Javascript - treats a line break as semicolon if the next nonspace char cannot be a continuation of the current statement.

It might be useful to write in the defensive style by adding semicolon before symbols (, [, / 

```js
let x = 0                         // Semicolon omitted here
;[x,x+1,x+2].forEach(console.log) // Defensive ; keeps this statement separate
```

The exception of the general rule is return, throw, yield break and continue. These will add semicolon whenever there is a line break

## 2. Type, Value and Variables
  
Data Type
- primitive: immutable data type: Boolean, Number, String, Null, Undefined, Symbol
- object: mutable types: others
  
function
```js
function fn1() {}

const fn2 = function() {};

const fn3 = () => {};
```

### 2.1. Variable Declarations
Variables
- let: re-assignable variable (ES 2015), re-declaration not allowed in the same scope
- const: const variable (ES 2015)
- var: old variable

#### 2.1.1. var
`var` variables have the `function` scope, 
- Variables declared with `var` are scoped to the body of the containing function
- if outside of a function, they are declared as a global variable, which is a property of `globalThis`

Unlike variables declared with `let`,  it is legal to declare same variables multiple times with `var`

`var` has an feature known as `hoisting`, where the declaration is moved to the top of the enclosing function.
Therefore variables declared with `var` can be legally used anywhere in the enclosing function.

```js
//The first one is processed as the second one
function f() {
    console.log(a+" World");
    var a="Hello";
}

function f() {
    var a;
    console.log(a+" World");
    a="World"
}
```

#### 2.1.2. let, const
`let` and `const` variables have the `block` scope

```js
// if no init value provided, its value is undefined
let i
```

They canot be decalred twice in the same block scope.


### 2.2. Primitive Types
JavaScript types can be divided into two categories: primitive types and object types. Primitive types are immutable, they are compared by value

#### 2.2.1. Number

#### 2.2.2. String

#### 2.2.3. Boolean

### 2.3. Object Types
Object types are mutable, they are compared by reference

```js
let a = {x: 1}, b = {x:1}
a === b // false

let c = a // assign same reference
a === c // true

{} === {} // false, different object
[] === [] // false, different object
```

#### 2.3.1. Object

##### Global Object
Global object is a regular JavaScript object, its properties are globally defined identifier that are available to a JavaScript program. (e.g: undefined, parseInt, Date())

- In node it is `global`
- In browsers, it is `window`
- `globalThis` can refer to the global object in any context

#### 2.3.2. Array

## 3. Concurrent Model
event loop

## 4. Reference
[1] Flanagan, David, and Will Sell Like. "JavaScript: The Definitive Guide, 7th." (2020).
[2] [A good online tutorial](https://javascript.info/)
[3] [A good Youtube video explaining the event loop, async in JavaScript (V8)](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=198s)
