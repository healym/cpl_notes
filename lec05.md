Lecture 5 - Python extras
=========================

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
