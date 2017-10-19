# JavaScript Basics


## Quick Facts

+ Dynamic, untyped, and interpreted
    - There is no compile step
    - **ALWAYS** use semicolons at the ends of statements
        * technically optional, but good style


+ comment lines begin with `//`
    - comment blocks start with `/*` and end with `*/`


+ `console.log()` is how you write to the console


+ You can declare/assign variables in several ways:
    1. `var x = 10;`
    2.
      ```
      var y;
      y = 10;
      ```
    3. `var w=10,v=10;`
 **ALWAYS** use `let` or `var` or `const` when declaring a variable,
 otherwise you pollute the global context.

### Note:
 variables are CaSe SeNsItIvE


## Types


### Primitive Types/Values
#### number
+ floating point


#### boolean
+ true/false


#### string
+ no char, just strings of length 1
+ use .length for string length


#### `null`
+ used in places where an object can be expected, but no object is relevant
+ There's only *one*
+ Today, it is rationalized that `null` is considered a placeholder for an
object, even though *technically* it is a primitive value
+ **NOT** an empty object


#### `undefined`
+ used in places where a variable has been declared, but not assigned
+ "error-like" absence of value
+ Returned from functions if no value is explicitly returned


### symbol
+ unique, immutable, primitive value


#### Object
+ A collection of properties
+ properties are pairings of key to value
    * key must be a strings
    * values can be anything
+ Object literal syntax:
    * `x = {id:5, name:"bob", dog:{}}`
+ Objects can be defined on-the-fly:

```
x = {};
x.id=5;
x.name = "fred";
x.dog = {};
```


### Assignment

Variables are dynamically typed


You can reassign a var to something of a different type

```
var x = 12;
console.log(typeof(x)); // number
x = "bob"
console.log(typeof(x)); // string
```
*aside: String is not string*


### Operators

#### `+`, `-`, `*`, `/`, `%`
+ `%` is remainder, not modulo
+ handles sign different

#### Compound Assignment
 `+=`, `-=`, `*=`, `/=`, `%=`


#### Increment/Decrement
`++`, `--`


#### Comparison
`>=`, `<=`, `<`, `>`, `==`, `!=`


### Here be Dragons:
```
var bar = 5;
bar += 2; // 7
var baz = true;
baz += 1; // true
var foo = true;
foo += false; // 1
1 + "foo"; // "1foo"
"foo" + false; // "foofalse"
"foo" + "bar"; // "foobar"
```


### Arrays

```
a = ["hey","there",,5];
console.log(a[0]); // "hey"
console.log(a[2]); // undefined
```


### Variable Hoisting
Variable declarations float to the top

Example: *(these two are logically equivalent)*
```
console.log(x === undefined); // true
var x = 3;
```

```
var x;
console.log(x === undefined); // true
x=3;
```

When scripts loaded, variable declarations are brought to the top


### Scope


Traditionally, blocks don't have scope, only functions do.

If you declare a variable in an if statement, it is visible to the whole function

`let` and `const` allow you to create block-scoped variables
