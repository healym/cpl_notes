---
layout: default
---

# Introduction

## History

Go was primarily designed for concurrent, server-side programming.
It was designed by Robert Griesemer, Rob Pike, and Ken Thompson, while they were working at Google. Some say Go is what C would have been, had it been developed today.

Go is very much used by Google, and many Go maintainers are employed by Google.

Go is an open source project with a BSD-style license.

### Other Quick Facts

Go is picky: if it's worth a warning, it's worth an error.
Things like unused variables, unused imports, and style violations will
cause errors.
There is no flexibility in style in Go. You must use tabs, not spaces,
and braces must start on the opening line, among other things.


Go has common design patterns, or idioms, that are recognizable:
- Getters don't need to start with `Get`
- Don't insert superfluous semicolons
- Use a switch statement over a long if-else chain
- the "comma ok" idiom


Misc Facts
Go is compiled, but small programs can be run with `go run`.
Build larger projects with `go build` or `go install`.
Install will make new directories to hold your binaries

Go is statically typed, meaning that types *cannot* change throughout the program.

Comments are the same as they are in C and C++

The compiler **will not** implicitly convert types.
There is no type coersion.


#### Go subcommands
- `go run` - compiles and runs in one step
- `go build`
- `go install`
- `go fmt` - formats your code
- `go doc` - displays package documentation

## What's so great about Go?
Many people find Go easy to read and write, it is a leader in concurrent programming, and it is garbage collected.

It is often used for network programming, or any other concurrent use case.

Go is *very very* good at running on multiple cores.

## Things to know
In CPL, we will use version 1.9.1, since new versions of Go deprecate older versions.

code can be tested [online](http://play.golang.org)

All code *must* be formatted with `gofmt`


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

## Appending to Slices
```go
func append(slice []T, elems ... T) []T
```

`append` is a built-in function that appends elements to the end of a slice.
If the slice has sufficient capacity, then the destination is resliced
to accommodate the new elements. If there isn't enough room, a new underlying
array will be allocated.

### Note:
append returns a _new_ slice, and it is necessary to hang on to the return value.

Example:
```go
s := []int{1, 2}
s = append(s, 3)
fmt.Println(s) // [1 2 3]
```

### Reallocating a slice
```go
s := []int{1, 2}
fmt.Println(s, len(s), cap(s)) // [1 2] 2 2

t := append(s, 3)
fmt.Println(t, len(t), cap(t)) // [1 2 3] 3 4

s[0] = 5;
fmt.Println(s, t) // [5 2] [1 2 3]
```


### Reslicing
```go
s := make([]int, 2, 10)
s[0], s[1] = 1, 2

fmt.Println(s, len(s), cap(s)) // [1 2] 2 10

t := append(s, 3)
fmt.Println(t, len(t), cap(t)) // [1 2 3] 3 10

s[0] = 5
fmt.Println(s, t) // [5 2] [5 2 3]
```

### Note:
It is idiomatic to catch the append with the same name as the slice, as if
you are appending the slice in place.

# Unicode

Unicode is a collection of symbols including letters, numbers, emoji,
accents, etc; its repertoire has more than 128,000 code points.

### Note:
a code point is not necessarily a character
(U+0041 is `A`, U+030A is `º`, U+0041U+030A is `Å`)

## Unicode Transformation Format

### UTF-32
+ Fixed width
+ Each code point is directly indexable
+ can be represented in Go as `[]rune`

### UTF-16
+ Variable width -> 16 or 32 bits
+ stored in Go as `[]uint16`

### UTF-8
+ Variable width -> 1, 2, 3, or 4 8-bit units
+ stored in Go as `[]uint8` or `[]byte` or `string`
+ the first 128 entries in the ASCII table correspond to UTF-8

Examples:
```go
u32 := []rune{'h','e','l','l','o','😐'}
fmt.Printf("%x\n", u32) // [00000068 00000065 0000006c 0000006c 0000006f 0001f610]

u16 := utf16.Encode(u32)
fmt.Printf("%x\n", u16) // [0068 0065 006c 006c 006f d83dde10]

u8 := utf8.Encode(u32)
fmt.Printf("%x\n", u8) // [68 65 6c 6c 6f f09f9890]
```

# Strings

A string is simply a slice of bytes. Go cannot and does not
guaratee that the slice will be ASCII encoded, UTF-8 encoded,
or anything else.

Go source code is UTF-8, so the source for string literals is UTF-8 text.
```go
s := "hello😐" // a UTF-8 encoded string
😺 := "valid" // a valid variable name
```

## Differences between `string` and `[]byte`
```go
r := 'o'
s := string(r)
t := []byte(s)

fmt.Println(s) // o
fmt.Println(len(s)) // 1
fmt.Println(t) // [ 111 ]

x := 'ö'
s := string(r)
t := []byte(s)
fmt.Println(s, len(s)) // ö 2
fmt.Println(t) // [195 182]
c = utf8.RuneCountInString(s)
fmt.Println(c)
```

# File I/O and Exception Handling

## Example
```go
package main

import(
  "fmt"
  "io/ioutil"
  "os"
)

func main() {
  contents, err := ioutil.ReadFile("file.txt")
  if err != nil {
    fmt.Println(err)
    os.Exit(1)
  }
  fmt.Println(string(contents))
}
```

## Exceptions
As you may have noticed in the example above, Go does not have exceptions.
Rather than raising an exception, functions typically return
an error value describing the problem encountered.

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


# Maps
Maps map keys to values, similarly to dicts in Python,
but with many more restrictions.


## Quick Facts
 - a map's zero value is `nil`
 - you cannot set/get values from nil
 - `len()` will give number of key/value pairs
 - `cap()` doesn't work

## Basic Usage
```go
var sounds map[string]string
sounds = make(map[string]string)

weights := make(map[string]float64)

sounds["frog"] = "ribbit"
weight["frog"] = 2.4
fmt.Println(weights) // map[frog:2.4]
```

### Map literals

```go
counts := map[string]int {"frog":2, "submarine":1}
names := map[string][]string {
  "frog": []string {"jim", "fred"},
  "submarine": []string {"bob"},
}

names["frog"] // {jim, fred}
names["cat"] // nil
```

## Working with Maps
Since exceptions do not exist in go, the `, ok` pattern is a common way
to deal with things that would raise an exception in other languages.

### `, ok`
```go
counts := map[string]int{"dogs":3, "cats":0}
counts["dinosaurs"] = 10
fmt.Println(counts["dinosours"]) // 10
delete(counts, "dinosours") // remove key-value pair

counts["giraffe"] // zero value for missing keys
if val, ok := counts["giraffe"]; ok {
  // case that the key exists
} else {
  // case that the key doesn't exist
}
```
The `, ok` pattern allows you to distinguish from a zero value
returned by the map, and a zero value returned because a key doesn't exist.


# Structs
A struct is simply a collection of fields:

```go
type Pony struct {
  Name           string
  Height, Weight float64
  FavoriteFoods  []string
}

func main() {
  dave := Pony{"Dave", 3.2, 100, []string{"pie"}} // using a struct literal
  alice := Pony{Name: "Alice", Weight:100, Height:3.2, FavoriteFoods:[]string{"kale"}}
  carol := Pony{Name:"carol"} // not all params need to be specified
  e := Pony{} // all values zeroed
  p := &Pony{} // *Pony
  p2 := new(Pony) // all values zeroed, as usual with new

  dave.Name = "Davey" // dot operator can be used to access
  p.Name = "Peter" // Go can implicitly dereference for this
}
```
As can be seen, structs can be defined with either an ordered literal,
or a literal with named arguments.

Structs can be output with `fmt.Println`, although there are other methods
with more convenient formatting.

## Methods
Go does not have classes, but _any_ type in Go can have a method.

```go
func (p Pony) PrintFavorites() {
  fmt.Println(p.Name, "likes", strings.Join(p.FavoriteFoods,","))
}

func main() {
  dave := Pony{"dave", 3.2, 100, []string{"carrot", "broccoli"}}
  dave.PrintFavorites() // dave likes carrot,broccoli
}
```

### Value Receivers
Methods with value receivers, as seen above,  operate on copies
of the original value.
Because of this, changing attributes of the received value does not
affect the original.

### Pointer Receivers
Methods with pointer receivers can modify the value to which the receiver
points. These are often more common than value receivers.
```go
func (p *Pony) AddFavorite(f string) {
  p.FavoriteFoods = append(p.FavoriteFoods, f)
}

func main() {
  dave := Pony{"dave", 3.2, 100, []string{"carrot", "broccoli"}}
  dave.AddFavorite("spaghetti")
  dave.PrintFavorites() // dave likes carrot,broccoli,spaghetti
}
```

# Exporting
In Go, rather than `public` and `private` sections, as in C++,
 items starting with a capital letter is exported by the compiler.

When importing a package, you can only access exported items.

Its that simple.

# Concurrency
Concurrency is the ability for a program to do multiple things
at the 'same' time.

When parts of code are running concurrently, you are often unable to determine
when things will happen and in what order.

## Goroutines
A goroutine is a lightweight thread of execution managed by the Go runtime.
Different from OS threads, they are independent, concurrent threads
of control which share the same address space.

When [main()] returns, the program exits. It does not wait for other (non-main)
goroutines to complete. This is fundamentally different than the model used in
Node.js.

### The `go` Keyword
A `go` statement starts the execution of a function call as a goroutine.
Unlike a regular call, program execution does not wait for the invoked
function to complete, as mentioned above.

```go
package main
import(
  "fmt"
  "time"
)

func say(s string) {
  for i:=0; i < 5; i++ {
    fmt.Print(s)
    time.Sleep(500 * time.Millisecond)
  }
}

func main() {
  go say("Hello ")
  time.Sleep(0.5 * time.Second)
  for i := 0; i < 5; i++ {
    fmt.Println("world!")
    time.Sleep(1 * time.Second)
  }
}
```
##### Output
```
Hello world!
Hello world!
Hello world!
Hello world!
Hello world!
```


## Channels
Channels are a primitive needed in order to communicate between goroutines.
You can send/recieve over a channel, in a first-in-first-out queue.
Channels can be buffered or unbuffered. An unbuffered channel-communication
succeeds **only** when a sender *and* receiver are both ready. In contrast,
a buffered channel succeeds without blocking if the buffer is not full when
sending, or not empty in the case of receiving.

### Quick Facts:
- A channel's zero-value is `nil`
- Channels must be initialized with `make()`

### Example(unbuffered):
```go
func print(strings chan string) {
  for {
    x := <- strings
    fmt.Println(x)
    // what follows is the idiomatic method:
    // fmt.Println(<- strings)
  }
}

func main() {
  c := make(chan string)
  go print(c)
  c <- "apple"
  c <- "banana"
  c <- "carrot"
}
```

### Example(buffered)
```go
c := make(chan string, IO)
c <- "apple"
c <- "banana"
c <- "carrot"

fmt.Println(<- c)
fmt.Println(<- c)
fmt.Println(<- c)
```

### Example with Concurrent Data Processing:
```go
package main
import (
  "bufio"
  "fmt"
  "io"
  "os"
)

func countWords(name string, success chan bool) {
  file, err := os.Open(name)
  if err != nil {
    fmt.Println(name, err)
    success <- false
    return
  }
  defer file.Close()
  scanner := bufio.NewScanner(file)
  scanner.Split(bufio.ScanWords)
  count := 0
  for scanner.Scan() {
    count++
  }
  if err := scanner.Err(); err != nil {
    fmt.Println(err)
    success <- false
    return
  }
  fmt.Println(name, count)
  success <- true
}

func main() {
  files := []string{"data1.txt", "data2.txt"}
  s := make(chan bool)
  for _, f := range files {
    go countWords(f, s)
  }
  for i := 0; i < len(files); i++ {
    <- s
  }
}
```

## Synchronization
There are several ways to use channels to synchronize goroutines
- using a channel to send results
- using a channel to signal completion
- `close()`

### The `close` Function
The close function is a builtin function that closes a channel
to indicate that nothing else will be sent over the channel.
Sending over a closed channel causes a runtime panic.
Receiving from a closed channel will give you a zero-value for the
channel's type.

#### Signaling End of Output
```go
func fib(n int, c chan int) {
    x, y := 0, 1
    for i := 0; i < n; i++ {
        c <- x
        x, y := y, x + y
    }
    close(c)
}

func main() {
    c := make(chan int)
    go fib(10, c)
    for i := range c {
        fmt.Println(i)
    }
}
```

##### Note: closed channels can be reopened with `make(chan [type])`

#### Signaling End of Input
```go
type Coord struct {
    x, y float64
}

func printDistance(coords chan Coord, done chan bool) {
    for c := range coords {
        fmt.Println("Distance", math.Hypot(c.x, c.y))
    }
    done <- true
}

func main() {
    c, d := make(chan Coord), make(chan bool)
    for i := 0; i < 3; i++ {
        go printDistance(c, d)
    }
    for i := 0; i < 10; i++ {
        c <- Coord{rand.Float64(), rand.Float64()}
    }
    close(c)
    for i := 0, i < 3; i++ {
        <- d
    }
}
```

## Select Statement
A select statement waits on multiple channel operations, and runs the first
communication operation that is ready. If multiple are ready, one is run
at random.

```go
func main() {
    c := make(chan int)
    quit := time.After(5 * time.Millisecond)
    go func() {
        for i := 0; ; i++ {
            c <- i
        }
    }()
    for {
        select {
        case val := <- c:
            fmt.Println(val)
        case <- quit:
            fmt.Println("quit")
            return
        }
    }
}
```

# Packages
You can break Go programs into smaller files and create packages.

### Example layout:
```
src/
	mypackage/
		stuff.go // package mypackage
		other.go
	myexec/
		main.go // package main
		helpers.go
```

##### Note: any buildable and executable Go code must be in package main

## Building and Running Go Programs
You can build your executable using either `go build myexec`
or `go install myexec`; in either case, you must set the `GOPATH` variable.
Everything in a package is accessible within the package itself; other
packages can only access exported items.


### Methods
A method can only be defined for types declared in the same package.
In addition, the receiver type of a method must be defined in the same
package as the method.

##### Note: method receivers cannot be an interface type.


# Interfaces
An interface is just a type that defines a set of methods.
Implementing an interface is a simple as implementing all of its methods.
A variable of interface type can store a value of any type with a method set
that is a superset of that interface.

### Quick Facts
 - Interfaces are usually named [type]er
 - The zero-value of an interface is nil

## Method Sets
The method set of an interface type is its interface.
For any other type `T`, the method set consists of all methods
that are defined with receiver type `T`.
Pointers expand this. For example, the method set of type `*T` is the set
of all methods defined with receiver type `T` or `*T`. Because of this,
the method set for `*T` contains the members of the method set for `T`.

### Example:
```go
type Dog struct {
	stomach []string
}

func (d *Dog) Eat(food string) {
	d.stomach = append(d.stomach, food)
}

type Cow struct {
	stomachs [4][]string // Cows have 4 stomachs. Google it
}

func (c *Cow) Eat(food string) {
	c.stomachs[0] = append(c.stomachs[0], food)
	// The cow is a mysterious creature, and it will magically pass
	//	food from one stomach to the next. We will not implement this.
}

type Eater interface {
	Eat(string)
}

func FeedCorn(e Eater) {
	e.Eat("corn")
}

func main() {
	d := Dog{}
	c := Cow{}

	d.Eat("spaghetti") // { [spaghetti] }
	c.Eat("sandwich") // { [ [sandwich] [] [] [] ] }

	var e Eater
	e = &d // make d an Eater, since it has an Eat func
	e.Eat("kale")

	e = &c
	e.Eat("spinach")

	FeedCorn(&d) // { [spaghetti, kale, corn] }
	FeedCorn(&c) // { [sandwich, spinach, corn] [] [] [] }
	FeedCorn(e) // { [sandwich, spinach, corn, corn] [] [] [] }
}
```

## Implementing External Interfaces
Unlike methods, interfaces can be implemented outside of the package
in which they are defined. The only caveat is that you must import the
package in which it is defined, as should seem obvious.

### Example Interfaces
```go
// in "fmt"
type Stringer interface {
	String() string
}

// in "sort"
type Interface interface {
	Len() int
	Less(i, j int) bool
	Swap(i, j int)
}
```
#### Usage
```go
package main
import (
	"fmt"
	"sort"
)

type Pony struct {
	Name string
	Height, Weight float64
	Foods []string
}


func (p Pony) String() string {
	return fmt.Sprintf("%s(%f)", p.Name, p.Weight)
}

type Ponies []Pony

func (ps Ponies) Len() int {
	return len(ps)
}

func (ps Ponies) Less(i, j int) bool {
	return ps[i].weight < ps[j].weight
}

func (ps Ponies) Swap(i, j int) {
	ps[i], ps[j] = ps[j], ps[i]
}

func main() {
	ranch := make(Ponies, 100)
	for i := range ranch  {
		ranch[i].Name = fmt.Sprintf["p%d", i]
		ranch[i].Weight = float64(i%3)
	}
	fmt.Println(ranch)
	// [p0(0) p1(1) p2(2) p3(0) ...]
	sort.Stable(ranch) // works, since ranch implements sort.Interface

	fmt.Println(ranch)
	// [p0(0), p3(0), p6(0), ...]
}
```

## Empty Interface
The empty interface is the interface type that specifies 0 methods.
It looks like this:

```go
interface{}
```

Every type implements the empty interface because every type has
at least zero methods in its method set.
Since every type implements the empty interface, we can store anything
there, like `void*` in C++, but less weird.

```go
func describe(thing interface{}) {
	fmt.Printf()"%v;%T\n", thing, thing)
}

func main() {
	var i interface{}
	fmt.Println(i)

	i = 5

	describe(i)
}
```

### Casting Empty Interfaces back to Other types

```go
var i interface{} = hello
s := i.(string)
fmt.Println(s) // hello

f := i.(float64) // panic
f, ok := i.(float64) // no panic, ok is false
```
This is alright, but would be tedious in practice.
Enter the type switch.

### Type Switches
A type switch takes an interface and matches cases based on its type
```go
switch v := i.(type) { // i.(type) MUST be written like this
case int:
	// v is an int
case string:
	// v is a string
default:
	// v is an empty interface
}
```
Ahh, much better.
