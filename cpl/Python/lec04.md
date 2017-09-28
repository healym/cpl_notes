Built-in Functions
==================

-------------------------------------------------------------

Built-ins
---------

+ `sorted(iterable [,key] [,reverse] )`
  - Returns a _new_ sorted list based on the `iterable` in ascending order
  - Example:
    ```
        x = [3,1,2]
        y = sorted(x)
        print(y) #[1,2,3]
        print(x) #[3,1,2]
    ```
    - `.sort()` sorts in place


+ `len(thing)`
  - Returns the length of `thing`
  - Works on strings, dictionaries, lists, tuples, and some other types, too


+ `help(object)`
  - Opens documentation for `object`
  - really useful in the interpreter
  - Quit with `q`


+ `enumerate(iterable, start=0)`
  - returns an object of type enumerate
    * yields tuples: (index, value)
  - keeps track of indices of object
  - Example:
  ```
  for i,l in enumerate(something):
    print( l," is at index", i)
  ```


+  `range([start,] stop [,step=1])`
  - Returns an object of type range
    * represents an immutable sequence of numbers
  - Useful for looping a set number of times
  - Don't use this as a crutch
  - Bad:
  ```
  L = [1,2,3]
  for i in range len(L):
    print(L[i])
  ```
  - Good:
  ```
  L = [1,2,3]
  for i in L:
    print(i)
  ```
  - Using range adds bloat if you don't need it
  - To mutate list:
  ```
  L = [1,2,3]
  for i,v in enumerate L:
    print(v)
    L[i] = 10
  ```
    * Gives you indices without garbage and calculating length


+ `input( [prompt] )`
 - like cin; prompts the user for input
 - reads from stdin


+ "Constructors"
 - `int()`, `float()`, `str()`, `dict()`, etc.
 - Example: `int(something_that_is_not_an_int)`
 - Pitfalls:
    * `int("100.0")` will not work
    * `int(float("100.0"))` will work

Defining Functions
------------------

+ Basic syntax:
  ```
  def <function name>(<arguments>):
        <body>
    ```

+ Arguments
 - Values must be provided for each positional argument in order
 - Arguments are always "[passed] by object reference"
  * wat. _**Prime test material**_
  ```
  def func(a):
    a.append("frog")
    a = ["giraffe"]
    a.append("submarine")
 x = ["apple"]
 y = x
 func(y)
 print(x) #[ "apple", "frog" ]
 ```


+ A function _always_ returns something
 - If not explicitly, will implicitly return None.


Code Examples
-------------

+ Loops cont.
 - skipping values
