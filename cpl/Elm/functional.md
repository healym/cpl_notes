---
layout: default
---
# Functional Programming

## Models
Applications are stored as a data structure that stores the *state*.
Every time an event happens(a function is called), a *new* state is generated,
based upon the event, and the current state.

## State
In Elm, your code cannot change state, which means that you cannot modify
variables, and there are no loops, only recursion.


# Syntax

## Type Annotations
```elm
--Value
pi : Float
pi = 3.14

--Function
minus : Int -> Int -> Int
minus x y = x-y

add : Int -> Int -> Int -> Int
add a b c = a+b+c

sin : Float -> Float

```

## Higher Order Functions
```elm
flip : (a -> b -> c) -> b -> a -> c
flip f x y = f y x

g : Int -> Int -> Int
g = flip minus
```

## Union Types
Union types represent more than one possible value.
```elm
type Bool
	= True
	| False

type Thing
	= A
	| B
	| C
	| D
```

### `type Maybe`
The maybe type represents a value that may or may not be there.
```elm
type Maybe a
	= Just a
	| Nothing

List.head : List a -> Maybe a
```
### `type Result`
The result type represents either a success of a failure.
```elm
type Result err value
	= Ok value
	| Err err

toInt : string -> Result String Int
```
