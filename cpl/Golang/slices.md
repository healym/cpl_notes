# Slices cont.

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
