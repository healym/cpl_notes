# Control Flow

## More on Comparison

+ Objects are converted to primitive types if compared with a primitive

+ Objects are compared according to their memory address (by reference, much like `is` in Python)


## Control Structures


### Block Statements


#### Conditionals

```javascript
{
  anything goes here
}
```
+ If/Else
    ```
    if(stuff()) {
      //stuff
    } else if (other_stuff()) {
      //other stuff
    } else {
      even more stuff
    }
    ```


+ Switch Statements
    - Fallthrough as in C++
    - can use strings


  ```javascript
  switch(expr) {
    case label1:
      statement;
    case label2:
      statement;
      break;

    // other cases could be included

    default:
      statement;
  }
    ```


#### Looping Constructs

##### For loops
```javascript
for(let i=0;i<10;i++) {
  // i exists
}
// i does not exist
```


##### Do-While
```javascript
do {
  // stuff
} while(expr);
```


##### While
```javascript
while(expr) {
  // stuff
}
```


##### For..in
  - iterates over all enumerable and distinct properties of an object
    in *original insertion order*

  ```javascript
  let obj = {b:2, c:3};
  obj.a = 1;
  for(let x in obj) {
    console.log(x);
  }
  // b
  // c
  // a
  ```

  ```javascript
  lst = ['h', 'e', 'l', 'l', 'o'];
  lst.name = 'hello';
  for(let x in lst) {
    console.log(x)
  }
  // 0
  // 1
  // 2
  // 3
  // 4
  // 'name'
  ```
  this weirdness is because for..in iterates over *enumerable* elements, like
  indicies


##### For..Of
  - iterates over elements of an iterable object including Array and string

  ```javascript
  let arr = [3, 5, 7];
  arr.foo = 'bar';

  for(let x of arr) {
    console.log(x);
  }
  // 3
  // 5
  // 7
  ```

  ```javascript
  for(let x of "abc") {
    console.log(x);
  }
  // a
  // b
  // c
  ```


##### `forEach` Method of Array
  ```javascript
  let arr = [3, 5, 7];
  arr.forEach(function(value) {
    console.log(value);
    });

    // 3
    // 5
    // 7
  ```


##### Break and Continue
- `break` breaks innermost enclosing loop statement
- `continue` skips to next iteration of innermost enclosing loop statement


##### Labels

    ```javascript
    thing: // this is the label
    while(stuff) {
      // other stuff
    }
    ```

    - allows breaking or continuing out of outer loops
    - does **not** allow `goto`, nor anything like it


## Functions
```javascript
'use strict';
function multiply(a, b) {
  return a * b;
}

multiply (5, 2); // 10

multiply(3, 5, 4); // 15, ignores everything else

multiply(5); // NaN
```

### Facts
+ No function overloading
+ Functions are first class because they are objects
    - Functions can have properties
    - Functions can be passed as a parameter
    - Functions can be returned from other functions
    - JavaScript has higher order functions!


## Extra Bits

### False-y Values
+ `false`
+ `null`
+ `undefined`
+ `0`
+ `NaN`
+ `""`

### Using `typeof`

this is an operator

`console.log(typeof 'frog'); // string`

`console.log(typeof 12); // number`
