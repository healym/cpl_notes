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
