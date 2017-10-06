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
