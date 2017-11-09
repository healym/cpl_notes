---
layout: default
---

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
