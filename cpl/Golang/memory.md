---
layout: default
---

# Memory and More

## Variables

### Note:
Because unused variables are a compiler error,
it is common practice to declare variables right before their use.
It is generally a waste of time to try to declare all variables at the
top of a function.

**Constants** are declared in much the same way as variables, but cannot be changed once declared.
### Note:
unused constants are *not* an error.

Example of constant declaration:
```go
const A = "frog"
const B string = "frog"
const (
  x string = "frog"
  y int = 10
  z = false
  )
```


## Pointers

A pointer(dereferenced by `&`) stores the address of a variable of a given type,
with the zero-value `nil`. Go does not permit pointer arithmetic.
```go
var x *int // a pointer named x that points to an int
var y *[3]int // a pointer named y that points to an array of 3 ints
```

As can be seen below, assignment in Go is a deep copy.

```go
package main
import "fmt"

func main() {
  x := [3]int {1,2,3} // [3]int
  y := x // [3]int
  fmt.Println(x) // [1,2,3]
  fmt.Println(y) // [1,2,3]

  y[1] = 10

  fmt.Println(x) // [1,2,3]
  fmt.Println(y) // [1,10,3]
}
```


## Memory Allocation
Question: How do i know if my variables are on the heap or stack?

Answer: It doesn't matter; don't worry about it.

The compiler runtime and garbage collector will handle all of that for you.

### `new(T)`
`new(T)` allocates storage for a variable of type T at runtime.
It returns a pointer(`*T`) pointing to the allocated variable, at points to a
zeroed value.

Examples:
```go
x := new(int) // *int -> allocated int
var y *int // nil
```

```Go
func main() {
  x := new([3]int)
  y := x
  y[1] = 5
  fmt.Println(x) // [0,5,0]
  fmt.Println(y) // [0,5,0]
}
```

### `make(T, args)`
`make(T, args)` creates slices, maps, and channels.
Slices, maps, and channels all require an array being allocated in the
background, which make can handle. Because of this, it returns an initialized
value of type `T`, *not* `*T`.

```go
func main() {
  x := make([]int, 3, 10) // []int <make(type, length, capacity)>
  y := x
  y[1] = 5
  fmt.Println(x) // [0,5,0]
  fmt.Println(y) // [0,5,0]
}
```

Confused? This is because x is a slice, which contains a pointer.

### Slices
A slice can be represented by this table:

|pointer|
|-------|
|length|
|capacity|

#### Slice Indexing
- Indexes in slices must be non-negative ints
- accessing index x or array/slice A outside of its range causes
a runtime panic
  + runtime panics are *not* like errors, they are treated as
  being much more serious, and should *not* be a part of your program

#### Creating Slices
literal slices:
```go
s := int[]{1,2,3,4,5} // literal slice
s[0] // 1
s[1:3] // [2,3] <- slice
len(s) // 6
cap(s) // 6
```

slices made with `make`:
```go
s := make([]int, 6, 10)
s[0] // 0
t := s[1:3]
len(s) // 6
cap(s) // 10

len(t) // 2
cap(t) // 9
```

Slicing arrays and slices:
```go
a := [8]int{1,2,3,4,5,6,7,8}
s := a[2:len(a)-2]

fmt.Println(s) // [3,4,5,6]
s[0] // 3
t := s[!:3]
fmt.Println(t) // [4,5]
len(t) // 2
cap(t) // 5
s[4] // panic
```
