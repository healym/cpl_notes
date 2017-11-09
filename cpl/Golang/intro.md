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
