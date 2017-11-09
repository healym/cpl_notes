---
layout: default
---

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
