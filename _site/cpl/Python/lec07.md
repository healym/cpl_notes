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
