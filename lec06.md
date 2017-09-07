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
