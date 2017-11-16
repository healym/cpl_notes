---
layout: default
---

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
