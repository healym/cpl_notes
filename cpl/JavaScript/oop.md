# Object-Oriented Programming

## Prototypes, Not Classes
JS does not have classes, per se
It is prototype oriented.

Instead of defining a class, we build up a 'prototype.'

We will still refer to the new types we define as classes, but keep in mind that they are not like classes in C++ or Python.

## The `class` Keyword
JavaScript classes were introduced in ES6 and they are syntactical sugar over JavaScript's existing protype based inheritance.

The class syntax is not introducting a new object-oriented inheritance model to JavaScript.

## Constructors
A constructor in JavaScript is 'just' a function that happens to be called with the `new` operator.

JavaScript uses functions as constructors for objects.

Define a function to start working on a new type.

Example:
```
var Frog = function() {
  // this example does nothing and has no properties
};

var jim = new Frog();
console.log(jim); // Frog{}
```
Example with attributes:
```
var Frog = function(name) {
  this.name = name;
};

var jim = new Frog('jim');
console.log(jim); // Frog{name:'jim'}
```

### Behind the Scenes

when you use the `new` keyword, it creates a new object within the scope of the constructor known as this, which is returned at the end of the function.

### Note:
`typeof(jim); // 'object'`

This is the case for any custom object in JavaScript.

## Adding methods to objects
```
var Frog = function(name) {
  this.name = name;
  this.x = 0;
  this.y = 0;
};

Frog.prototype.hopNorth = function() { // the prototype attribute must be modified
  this.y++;
};

Frog.prototype.hopSouth = function() {
  this.y--;
};

Frog.prototype.hopEast = function() {
  this.x++;
};

Frog.prototype.hopWest = function() {
  this.x--;
};

var jim = new Frog('jim');
console.log(jim); // Frog{name:'jim', x:0, y:0}
jim.hopNorth();
console.log(jim); // Frog{name:'jim', x:0, y:1}
```

### Note:
Methods added will still be callable on objects instantiated before the methods were added.

## On Inheritance
If you want to do any inheritance, assign methods to a type's prototype as shown previously.

JavaScript permits single-inheritance.

Search 'prototype chain' for more information.
