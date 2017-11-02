# Maps
Maps map keys to values, similarly to dicts in Python, but with many more
restrictions.


## Quick Facts
 - a map's zero value is `nil`
 - you cannot set/get values from nil
 - `len()` will give number of key/value pairs
 - `cap()` doesn't work

## Usage Example
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
