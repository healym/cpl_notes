---
layout: default
---

# Functions

Functions can take 0 or more arguments, the types of which come after the
variable names. Their return type comes at the end of the declaration,
opposite of the convention present in C++ and similar languages.
An absence of return type indicates that there is *no* return type. It should
also be noted that arguments are pass by value. It works exactly as you think
it should.

### Note:
Since there is no pass by reference, if you need to change a value in the
calling function, you must use a pointer.

## Function Definitions

### Example:
```go
package main

import "fmt"

func add(x int, y int) int {
  return x + y
}

func main() {
  fmt.Println(add(3, 5))
}
```

### Multiple Results
Functions can also have multiple returned values in Go
```go
func swap(x, y string) (string, string) {
  return y, x
}

func main() {
  a,b := swap("hello", "world")
}
```

### Named Results
Named results allow you to specify what you will be returning
in the declaration of a function.
```go
func f(val int) (x, y int) {
  x = val * 4/9
  y = val-x
  return // called a 'naked return'
}
```

## Defer
A defer statement defers the execution of a function until the
surrounding function returns.

### Example:
```go
func main() {
  defer fmt.Println("world")
  fmt.Println("hello")
}
```
##### Output
```
hello
world
```

### Note:
deferred calls' arguments are evaluated immediately.
```go
func f() string {
  fmt.Println("Beep")
  return "world"
}

func main() {
  defer fmt.Println(f())
  fmt.Println("hello")
}
```
##### Output
```
Beep
hello
world
```

### Stacking Defers
`defer` calls are placed in a stack, which becomes apparent when you call them
multiple times
```go
func main() {
  fmt.Println("counting")
  for i := 0; i < 10; i++ {
    defer fmt.Println(i)
  }
  fmt.Println("done")
}
```
##### Output
```
counting
done
10
9
8
7
6
5
4
3
2
1
0
```
### Use Case
`defer` is usually used as a clean-up action to be performed after
some other action is done, similar to context managers in other languages
```go
func main() {
  tmpfile, err := iotuil.TempFile("","example")
  if err != nil {
    log.Fatal(err)
  }
  defer os.Remove(tempfile.Name())
  // using tempfile
}
```

## Passing Pointers

```go
package main

import "fmt"

func f(x int) {
  x++
}

func g(x *int) {
  (*x)++
}

func main() {
  var a,b int
  f(a)
  g(&b)
  fmt.Println(a, b) // 0, 1
}
```

## Function Values
In Go, functions are values, and can be passed/returned to/from
other functions.

```go
package main

import (
  "fmt"
  "math"
)

func compute(fn func(float64, float64) float64) float64 {
  return fn(3, 4)
}

func main() {
  hypot := func(x, y float64) float64 {
    return math.Sqrt(x*x, y*y)
  }
  fmt.Println(hypot(5,12)) // 13
  fmt.Println(compute(hypot)) // 5
  fmt.Println(compute(Math.Pow)) // 81
}
```


## Function Closures
By using function closures, a function can still reference variables from
an outer function's scope, even after the outer function has returned.

```go
package main

import "fmt"

func adder() func(int) int {
  sum := 0
  return func(x int) int {
    sum += x
    return sum
  }
}

func main() {
  a := adder()
  for i := 0; i < 10; i++ {
    fmt.Println(a(i))
    }
}
```

#### Output
```
0
1
3
6
10
15
21
28
36
45
```
