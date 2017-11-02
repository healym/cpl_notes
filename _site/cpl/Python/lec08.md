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
