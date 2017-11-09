---
layout: default
---

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
