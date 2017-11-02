# Functions

Functions can take 0 or more arguments, the types of which come after the
variable names. Their return type comes at the end of the declaration,
opposite of the convention present in C++ and similar languages.
An absence of return type indicates that there is *no* return type. It should
also be noted that arguments are pass by value. It works exactly as you think
it should.

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
