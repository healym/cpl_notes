# The JavaScript Engine


## Exports and Imports

ES6 added `export` and `import` keywords that make JS feel more like Python & co.

#### Note:
They **don't** work with *most* JS engines.

If you're going to use them, you need a transpiler such as Babel.

In CPL, we will only use `module.exports`.


## Function Closures

Functions have access to the scope above them.

Examples:
```javascript
let sum = 0;
function acc(num) {
  sum += num;
  console.log(sum);
}

acc(4); // 4
acc(5); // 9
sum = 0; // we don't want to be able to do this, but we can.
acc(3); // 3
```

```javascript
function acc(num) {
  let sum = 0;
  sum += num;
  console.log(sum);
}

acc(4); // 4
acc(5); // 5
sum = 10; // sum is not in scope, this is a problem
```

But, consider the following:
```javascript
function acc_factory() {
  let sum = 0;
  return function(num) {
    sum += num;
    console.log(sum);
  };
}

let acc = acc_factory();
acc(4); // 4
acc(5); // 9
```
What's different?

Immediately Invoked Function Expressions.

Since the inner function has access to the `sum` variable, we retain the ability to read from and write to `sum`.

However, running `sum = 10;` would still cause an issue, since we don't have access to sum, only the returned function does.

So how can we make `let acc = acc_factory();` look less weird?

like this:
```javascript
var acc = (function() {
  let sum = 0;
  return function(num) {
    sum += num;
    console.log(sum);
  };
})();
```

## Asynchrony

This is cool.
*Really* cool.

First, read up on what function call stacks are (I don't want to explain that, too).


Consider the following main.js:

```javascript
console.log('A');

set Timout(function() {
  console.log('B');
  }, 3000);

for(let i=0; i<5; i++) {
  console.log('C', i);
}
```
This outputs the following:
```javascript
A
C0
C1
C2
C3
C4
B
```

Wait, what?

Let's look at the status of the program as it steps through:

<< i don't wanna do this right now >>

### Note:
The event loop only adds things to the call stack when the call stack is empty.
This means that if there is an infinite loop in the IIFE, nothing the node API pushes on the event que will run.

This boils down to the following piece of advice:

Spend as little time on the stack as possible, so the event queue can do what it needs to when it wants.
