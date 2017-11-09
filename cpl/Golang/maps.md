---
layout: default
---

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
