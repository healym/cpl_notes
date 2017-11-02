# Language Quirks


## Documentation

+ Mozilla Developer Network
    - most sane option

## Strict mode
+ An opt-in variant of JS
    - can be applied to entire scripts or to certain functions
    - changes semantics for the better
        * change some identifiers into reserved words
        * make accidentally creating global variables impossible
            + `var` or `const` required
        * function parameters must be unique
    - Use: `node --use-strict`
        * Alternatively, put `"use strict";` at top of script

```javascript
"use-strict"
yield=10; // error
y=10;     // error

function f(a,a,b) {   // not allowed
  console.log(a,a,b); // in strict mode
}
```

## Scope

Traditionally, only functions have scope.
As a result, variables defined in a block are visible to the entire function. This is done via 'variable-hoisting.'

`let` allows variables to be block-scoped (`let` can't be hoisted):
```javascript
function f() {
  var x = 1;
  if(true) {
    var y = 2;
    let z = 3;
    console.log(x,y,z); // 123
  }
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // ReferenceError
}

f();
```


## Assignment
+ Variable Assignment is 'pointer-y'
    - references in the same way as python:
    ```javascript
    var x = [];
    var y = x;
    x.push("frog");
    console.log(y); // ['frog']
    ```


## Primitive Types
+ data that is not an object and has no methods
    - `string`, `number`, `boolean`, `null`, `undefined`, `symbol`
    - all are immutable

#### Note:
`typeof(null)` is object.
This is widely recognized as a language bug.

## Primitive Wrapper Objects

`"frog".toUpperCase(); // "FROG"`

+ JS creates new object to perform method on
+ Each has it's own type
    - String for string
    - Number for number
    - Boolean for boolean
    - Symbol for symbol

`typeof(String("frog")) // string`

`typeof(new String("frog")) // object`

#### Note:
Primitive values are not objects.

## Objects
Most values in JavaScript are objects or can be used as objects.
+ This includes Primitive wrapper objects
+ Arrays
+ Functions
+ Regular Expressions


## Comparison

When two operands are of different types, one of them will be converted to an "equivalent" value of the other operand's type.

This is ridiculous.

This is also 'type coercion'.

#### Rules
+ Equality(`==`)
    - converts the operands to the same type *prior* to comparison
    - uses Abstract Equality Comparison Algorithm
    - rules for coercion are based on type
    - not always the right operand that is converted
    ```javascript
    1 == 1 // true
    1 == "1" // true
    "1" == 1 // true
    0 == false // true
    0 == null // false
    0 == undefined // false
    null == undefined // true
    ```


+ Inequality (`!=`)
    - complement of equality


+ Identity/Strict Equality(`===`)
    - only returns true if operands of the same type
    ```javascript
    3 === 3 // true
    3 === "3" // false
    ```


+ Non-Identity/Strict Inequality(`!==`)
    - complement of identity


##### Specific Rules:
+ number & string: string -> number
    - Nan is a number, false will always be returned


+if an object is compared to a string or a number, JS is going to try to use the `toString` method or `valueOf` method. Otherwise an error is generated.
