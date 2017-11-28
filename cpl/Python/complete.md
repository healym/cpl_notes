---
layout: default
---

Intro To Python
===============

 + version
   - using 3.5.2
	 - on lab boxes
	 - diff 2<->3
	 - unicode support
	 - backward incompatible changes to syntax and default libraries

quick facts
-----------

+ comments - lines start with #

+ print()
	- prints a value to console over stdout
	- same as cout

+ declare and assign in a single step
	x = 5, **not** int x; x = 5;

no compile step

Types
-----

+ Numbers
	- Int (Integer) - 5,6,7,etc
	- Float (Floating point) - 5.6

+ Boolean
	- True
	- False

+ str - String
	- single or double quotes
	  * "frog", 'frog'
	  * '',""
	  * "frog's leg" <-- double quotes good for apostrophe
	- Iterable
	- **no** character type, just single-char strings

+ None
	- None

Built-in Data Structures
------------------------

## List (list)

- Iterable
- Mutable sequence of elements
	* x=[1]
	* x.append(2) -- x==[1,2]

- Elements may be of differing types
  * Ex:
		```
		[1,2,3]
		[1,2,3,"frog"]
		[]
		```

- Indexing
	* begins at 0
	* index must be an Int

- slices
	* x[0:2] [included(0):**excluded**]
	* returns a **shallow** copy
	* start copying at the first slice index
	* stop before end
	* x[3:1] --[], needs other parameter to step backwards
	* x[3:3] --[], evaluation stops before including first element

- Negative indexing
	* counts from end of list
	* x[-1] --last element


## Tuple (tuple)

- Iterable
- immutable sequence of elements
- elements *can* have different types
- (x,) -- comma **required**
- () -- valid tuple, for some reason
- tuples can contain other tuples
- lists in tuples can be modified
- slicing
	works the same as a list


## Dictionary (dict)
- heavily abused
- Iterable(key by default)
- maps keys to values
	* both keys and values can vary in type
- _**not**_ a sequence
	* cannot depend on keys in any order
- examples:
	```
	x={'a':'frog','b':'giraffe','c':'apple'}
	x['a'] -- "frog"
	x['nope'] -- KeyError
	```


## Custom Types
- they exist
- Python has class-based objects


Assignment
----------

- Variables are _dynamically_ typed
	* It'll let you do this
	* It'll work
		 * Until it doesn't.


Unpacking
---------

- multiple assignments on one line
	 * ex
		 ```
		(a,b) = (1,2)
		a,b = 1,2
		a,b = [1,2]
		a,b = b,a
		```

- numbers need to match
	* a,b,c = 1,2 --PROBLEM
Operators, Control Statements, and Loops
========================================

Assignment _cont._
------------------

+ Python is sort-of pointer-y
 - example:
    ```
    x = []
    y = x
    y.append("frog")
    print(x) #["frog"]
    print(y) #["frog"]
    ```

Operators
---------

+ Arithmetic
 - `+`,`-`,`/`,`*`
 - `/` <- floating-point division
   * 5/2 -> 2.5
   * 5.5/3.3 -> 1.66667
 - `//` <- floored quotient
 - `**` - power
 - `+=`, `-=`, `/=`, `//=`, `*=`, `**=`
 - _**There is no `++` nor `--`**_


+ relational
    * ==,!=,>=,<=,<,>


+ logical
    * `not` -> like ! (there is no ! in Python)
    * `or`  -> like ||
    * `and` -> like &&


+ membership operator
    * `in`
    * returns `True` or `False`
    * `x in y` returns `True` if x is a member in y,
       otherwise returns `False`
    * Example:
    ```
    x = [ 1,2,3,4 ]
    4 in x #True
    50 in x #False
    y = {'a':10,'b':50}
    'a' in y #True
    50 in y #False, 50 is not a key
    50 in y.values() #True
    ```


+ is
  - Returns `True` or `False`
  - Tests object identity
  - _Don't use it unless you have a good reason to._
  - not the same as `==`
  - okay to use to compare with `None`
  - Pyflakes recommends using `is` with `True` and `False`
    * don't


Control Statements
------------------

  + `if` / `elif` / `else`
    - Example:
    ```
    if x == 5:
        stuff() #called the body
    elif x == 6:
        stuff()
    else:
        stuff()
    ```
    - No parentheses around expression
    - don't forget colons
    - no curly braces -> watch your indentation
      * Python is whitespace delimited


Truthiness/Falsiness
--------------------


  + Falsey values
    - False
    - None
    - numeric zero
    - ""
    - empty built-in data structures


  + Truthy values
    - True
    - not Falsey


  + `bool()`
    - `bool(truthy) #True`
    - `bool(falsey) #False`


  + be careful when comparing against True and False using `==`
    - `1 == True #True`
    - `[] == False #False`
    - `bool([]) == False #True`
    - aside from numeric types, objects of different types
      do not compare equal
    - _**Prime**_ test material


Loops
-----

  + `while`
    - pre-check loop
      * no post-check loop
    - leave parentheses off of expression
    - don't forget the colon


  + `for`
    - _different than c++_
    - Iterable -> can iterate with `for`
      * Iterator object can yield/return its members
        one at a time
      * File objects are iterable
    - `for <var> in <iterable>:`
    - `for x in range():`
    - leave parentheses off of expression
    - don't forget the colon
    - break
      * breaks out of the innermost loop
    - continue
      * continues to next iteration of loop
    - pass <- placeholder
    - else
      * executes if loop completes uninterrupted
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
Exceptions and File I/O
=======================

Documentation
-------------

### Docstrings
 + Ex:
 ```
 def send_message(sender, recipient, message_body, priority=1):
     """Send a message to a recipient

     :param str sender: The person sending the message
     :param str recipient: The recipient of the message
     :param str message_body: The body of the message
     :param priority: The priority of the message, can be a number 1-5
     :type priority: integer or None
     :return: the message id
     :rtype: int
     :raises ValueError: if the message_body exceeds 160 characters
     :raises TypeError: if the message_body is not a basestring
     """
     # Function definition
 ```
 + expected to document code on class assignments
 + generates web pages and stuff


Exception Handling
------------------

### Error types
+ Syntax errors
    * your code is bad and you should feel bad
    * Python cannot read it
    * Syntax check prior to interpreting code
+ Runtime Errors
  - Syntax is fine, logic is bad
  - Python can't execute it
  - Ex:
    ```
    for x in [1,2,3]:
        pront(x)
    ```
  - Not found until code is interpreted
  - RaiseExceptions


### Handling?
+ whenever a runtime error occurs, an exception is raised

+ helps us track down and fix logical errors

+ How they work:
 - whenever an exception is raised, it "bubbles up" through the call stack until it is caught *or* it reaches the top of the call stack
+ Ex:
```
def print_name(person):
    try:
        print(person["name"])
    except KeyError:
        print("Person has no name.")
```
+ All exceptions are instances of classes that derive from BaseException

+ Most exceptions you'll use derive from Exception

+ There's a big list of built-in exceptions
 - You can also define your own.


+ You can keep the caught exception as a var
 - useful for errors & debugging
 - Ex:
```
 try:
     f = open("file.txt")
 except FiltNotFoundError as e:
     print("Caught:",e)
 else:
     #runs if no exceptions raised and handled
 finally:
     #runs no matter what
```


+ Raising exceptions
 - ```raise valueError("Frog")```


 File I/O
 --------

 ```
 f = open.("file.txt")
 contents = f.read()
 print(contents)
 f.close()
 ```
### or

 ```
 with open("file.txt") as f:
     print(f.read())
#with closes automatically when you outdent
```
Lecture 6 - Modules and Classes
===============================
------------------------------------------------------------------------------

Modules
---------

+ Python projects can be split into multiple files
    - These are known as 'modules'
    - Code can be imported ```from``` one module to another
    - Modules can be used like libraries or like a program


+ Importing Modules
    - Import the whole module and access members with .
    - Import specific things from a module
    - The import process requires running imported modules
    - Use ```if __name__ == '__main__':```
        * Lets module work as library and as a program.

Classes
-------

+ Generally written in their own module
    - class Dog --> Dog.py


+ ```self``` is the calling object
    - You must use ```self``` to refer to member funcs/vars in class def
    - similar to ```this``` in C++/Java


+ Member functions are called methods


+ There are __no__ private members
    - The convention for "don't touch this" is naming with ```_``` before the name


+ Special methods usually are wrapped with ```__```
    - used to "overload" operators
    - used by constructors


Example:

```


class Dog:
    """A dog class"""

    def __init__(self, name, weight):
        """Dog constructor"""
        self.name = name
        self.weight = weight

    def bark(self):
        """Make noise"""
        print("BARK I AM", self.name, "BARK BARK!")

    def eat(self, food):
        """Eat some food.

        Gains one pound for every character in the name of the food.

        :param str food: The name of the food.
        """
        self.weight += len(food)

    def as_dict(self):
        return {"name": self.name, "weight": self.weight}

    def __lt__(self, other):
        return self.weight < other.weight

    def __str__(self):
        return "{0} ({1})".format(self.name, self.weight)


def test_dog():
    frank = Dog("Frank", 75)
    frank.bark()
    frank.eat("spaghetti")
    print(frank.as_dict())

    barney = Dog("Barney", 100)

    print("frank < barney:", frank < barney)

    print("barney < frank:", barney < frank)

    print("frank > barney:", frank > barney)

    print("frank >= barney:", frank >= barney)

    s = str(frank)
    print("s:", s)

    print("frank looks like...")
    print(frank)


if __name__ == "__main__":
    test_dog()


```


+ Custom Exception classes
    - often very simple:

```
class MyError(Exception):
    pass
```

__*pass is a no-op placeholder.*__
Python - *advanced* Python
==========================

Argument Lists
--------------

### Variable Argument Lists

```
def custom_print(*args):
    for i in args:
        print("output:", i)
```


### Keyword Arguments

```
def custom_print2(**kwargs):
    for k,v in kwargs.items():
        print("{}:{}".format(k,v))


>>>custom_print2(ocelot="awesome", warbler="bird")

ocelot:awesome
warbler:bird
```


Star Magic
----------

```
func1(a=10),c=12,b=13)
args = ["apple", "banana", "dog"]

func1(args) #not enough parameters

func1(*args) #a is "apple", b is "banana", c is "dog"
```

* Length of list must agree with number of parameters to function

```
d = {'a':10,'b':12, 'c':13}

func1(d) #not enough parameters

func1(**d) #a to 10, b to 12, c to 13
           #based on keyword, NOT position
```

#### Tips and Tricks

* Don't use star magic without a _good reason_

* Star magic will _not_ be required for CPL assignments

* Keyword parameters must come after positional parameters

* Arbitrary arg list comes after positional args, but before kwargs

* Arbitrary keyword arg lists come after listed keyword args
    - Ex: ```def func(a, b, *args, d=10, e=11, **kwargs)```


Generator Functions
-------------------

* Easy way to make a custom iterable

* When called, returns an object of type 'generator'

* Like any iteragle, yields one item at a time

* Determines next item on-the-fly

* Cannot index or slice generator objects

```
def count_forever(start=0):
    i = start
    while True:
        yield i
        i += 1
```

```
for x in count_forever():  #prints numbers up to ten
    print(x)
    if x == 10:
        break
```

* If execution of generator stops, acts just like end of list
    - In context of loop

```

def to_binary(it): #would have solved coding interview challenge in 3 lines...
    for x in it:
        yield bin(x)
```

```
g = count_to(10)
for x in g:
    print(x)

for y in g:
    print(x) #nothing will print, generator depleted
```

* Once generators are depleted, they can no longer return
    - This can be avoided by calling the function, rather than assiging and referring to an object

```
def first_n(num,it):
    '''Yields the first num items from it.

    '''
    counter = 0
    for x in it:
        if counter < num:
            yield x
            counter += 1
        else:
            break
```


### Generator Expressions

```
nums = (bin(x) for x in it) #it is an iterable, nums is a generator
```

```
nums = (bin(x) for x in range(5))
```

* Generator expressions can have filters:

```
nums = (bin(x) for x in range(5) if x % 2 == 0)
```

* Generator expressions can have multiple returns:

```
g = ((x,y) for x in range(3) for y in range(3))
```

This will act like nested for loops

```
g = ((x,y) for x in range(3) for y in range(x))
```

This makes weird garbage

* You can generate generators:

```
g = (((x,y) for x in range(3)) for y in range (3))
```


### List Comprehensions

```
[int(x) for x in ["10", "20"]]
```

List comprehensions are like generators that return lists


### Dict Comprehensions

```
{k: k.upper() for k in ["a", "b"]}
```

This is a thing I didn't know I needed.
Python - *advanced* cont.
================================

Higher Order Functions
----------------------

+ functions can:
    - accept functions as arguments
    - return functions as values

```
def is_even(x):
    return x % 2 == 0


def take_while(check,it): #accepts function check()
    '''yields items from it until check() returns False for some item'''
    for i in it:
        if check(i):
            yield i
        else:
            break


vals = [0, 2, 4, 6, 7, 8, 10]
list(take_while(is_even,vals)) #[0, 2, 4, 6]
```

```
def new_print(prefix):
    def inner(*args, **kwargs):
        '''
        assigns prefix passed to beginning of print,
        takes *args and **kwargs
        '''
        print(prefix,*args,**kwargs)
    return inner #returns function inner()


debug = new_print("debug: ")
#debug is new function that has "debug: " as prefix
warning = new_print("warning: ")

debug("reached here") #debug: reached here

warning("did the thing") #warning: did the thing
```


```
def f():
    i=0
    def g():
        print(i)
        return i
    return g


h=f()

h() #prints i, returns i


def f():
    i = 0
    def g():
        i += 1
        return i
    return g


h=f()
h() #Unbound local variable
```


Lambda functions
----------------

+ Lamdas are anonymous functions

+ Lambdas take zero of more arguments and return a values

+ That's it

+ Syntax: ```lambda [arglist]: expression```

    - ```lambda x: x + 1```
    - ```lambda x,y: x + y```

* Don't abuse them, only really used when you need a one-time function


```
dogs = [Dog("frank",150), Dog("bob",110),..] #not gonna write a whole list
# assume no __lt__
dogs2 = sorted(dogs) #TypeError

dogs3 = sorted(dogs,key=lambda x: x.weight) #extremely common usage

```


`map`, `filter`, and `reduce`
-----------------------

+ Holy trinity of math


+ All are higher order functions
    - work a lot like generator expressions


+ `map(func, iterable)`
    - returns a new iterable that yields func -> x for each x in iterable
    - `map(str,lst)` and `(str(x) for x in lst)` are about the same


+ `filter(func, iterable)`
    - returns a new iterable that yields x
    for each x in iterable if func(x) is truthy
    - `filter(is_even,lst)` and `(x for x in lst if is_even(x))`
    are similar


+ `reduce(func, iterable[,initial]) #import functools`
    - applies a function of two arguments cumulatively to the items
    of iterable from left to right so as to reduce the iterable into a single
    value
        * `vals = [0, 2, 4, 6]`
        ```

        functools.reduce(lambda x,y: x + y, vals) #12
        ```


Partial Function Application
----------------------------

Partially applies parameters to function, creates new function
that is already partly applied, so takes fewer parameters.

```
import functools

def add(x,y):
    return x + y

add3 = functools.partial(add,3) #partially applies 3 to add

add3(7) #10
```


Function Decoration
-------------------

+ Wraps a function to modify its behavior

+ Super common in Python Standard Library

+ Don't abuse these


```
import time

def time_this(func):
    def wrapper(*args,**kwargs):
        start = time.time()
        retval = func(*args,**kwargs)
        stop = time.time()
        print("{} took {:0.3f}sec".format(func.__name__,stop - start))
        return retval
    return wrapper
```

Extras
------

#### Ternery
+ works just like in c++
+ syntax:
 true ```if ``` condition ```else``` false
# CPL: Decorators to Decorators

## A study of higher order functions

## Abdirahman Ahmed Osman

## Pre-class

Consider theto_bin()andcount_forever()generator functions from class -
to_bin(it)returns an iterable that converts every item from _it_ to its binary rep-
resentation -count_forever(start = 0)return an iterable that yieldsstart,
start + 1,start + 2...

For each snippet, indicate whether it terminates or not

```
to_bin(count_forever())
(bin(x) for x in count_forever())
{x: bin(x) for x in count_forever()}
```
Define a function _count_ and a variable _init_ so thatreduce(count,my_list,
init) would return a dictionary indicating the number of times each item occurs
inmy_list.

```
from functools import reduce
# count definition
# init assignment
my_list = ['they','were', 'the', ....,'times']
reduce(count_my_list, init)
# {"best":1,"worst":1,"they":2...}
```
## Decorators and such

**def** time_this(func):
**def** wrapper(*args, **kwargs):
start = time.time()
retval = func(*args, **kwargs)
stop = time.time()
print("{} took {:0.3f}sec".format(func.__name__, stop-start))
**return** retval
**return** wrapper


@time_this
**def** add5(x):
time.sleep(1.0)
**return** x + 5

add5(10) _# return 15
# print:
# add5 took 1.001 sec_

deff add10(x):
time.sleep(2.0)
**return** x + 10

add10 = time_this(add10) _# same as putting @time_this before the function definition_

### Fun facts

- The@syntax is syntactic sugar forfunc = dec(func)
- You can stack multiple decorators!
    @
    @
    **def** func():
       **pass**
- You can decorate decorators
- A decorator will **clobber** a wrapper function’s docstrings,__name__, and
    other special attributes.
       **-** Usefunctools.wrapsto avoid this
          ∗it moves special attributes from function to the new wrapped
             function

### Validation

@validate_int
**def** prompt_for_age():
**return** input("Enter your age:")

prompt_for_age()
_# Enter your age: bob
# Requires int!
# Enter your age: 1_


Now let’s buildvallidate_int(func)

import functools

**def** validate_int(func):
@functools.wraps(func)
**def** wrapper(*args,**kwargs):
**while** True:
**try** :
integer_value == int(func(*args,**kwargs))
**return** integer_value
**except** ValueError:
print('Requires int!")
return wrapper

**Let’s make it more general**

**def** validate(const=int):
**def** decorator(func):
**def** wrapper(*args,**kwargs):
**while** True:
**try** :
**return** const(func(*args, **kwargs))
**except** ValueError:
print("Invalid value")
**return** wrapper
**return** decorator

@validate(float)
**def** prompt_for_age():
**return** input("Enter your age: ")

_# same as_
prompt_for_age = validate(float)(prompt_for_age)

## Packages

- Structure a python’s module namespace using “dotted module names”
    main.py
    classroom/
    __init__.py


```
utilities.py
modles/
__init__.py
assignment.py
```
- Inmain.py

```
import classroom.utilities
import classroom.modles.assignment
from classroom.models.assignment import Assignment
```
```
classroom.utilites.grade()
a = Assignment()
```
