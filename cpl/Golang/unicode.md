---
layout: default
---

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
