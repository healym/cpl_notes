# Go Basics


## Hello World:
```go
package main
import(
  "fmt"
)
func main() {
  fmt.Println("hello world")
}
```


## Variables
Variables are statically typed, and can be declared with
either explicit or implicit types, as shown below.


Explicit:
```go
var x int
var x, y, z int
var x, y, z int = 1, 2, 3
```


Implicit:
```go
x := 10 //int
x, y, z := 1, 2, 3 //ints
a, b, c := "a", 10, false //this works
```


## Built-in Types
`bool` can either be `true` or `false`

### Numeric types
  - unsigned integer types
    * `uint`, `uint8`, `uint16`, `uint32`, `uint64`
    * `uint` is 32 or 64-bit based on compiler implementation
  - signed integer types
    * `int`, `int8`, `int16`, `int32`, `int64`
    * `int` is either 32-bit or 64-bit depending on compiler implementation
  - IEEE-754 floating pt. types
    * float32
    * float64
  - Complex number types
    * complex64, complex128
  - Byte
    * alias for uint8
    * not converted to/from uint8 automatically
  - Rune
    * represents a Unicode codepoint (like a char, but not just ascii)
    * `rune` is an alias for `uint32`
    * again, there is no automatic conversion


### Strings
A `string` is a possibly empty sequence of bytes. They are immutable, and length can be checked via `len()`, similarly to Python.


### Arrays
Arrays are created by the syntax `[<number of elements>]<element type>`.
Arrays must be of constant size, are indexed at zero, and their length can be checked with `len()`, as one would expect.

### Slices
Slices are created using the syntax `[]<element type>`

They are defined as "...a descriptor for a contiguous segment of an underlying array..." by the documentation.
Slices are backed by an array with a set capacity, which can be checked with `cap()`.


### Absence of Value
`nil`.

That's it. It's just nil.


### Blank Identifier
`_` is used for ignoring unwanted values.
