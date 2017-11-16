---
layout: default
---
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
