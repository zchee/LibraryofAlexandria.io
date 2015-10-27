+++
categories = ["golang"]
date = "2015-10-27T16:57:41+09:00"
title = "cgo"

+++

# Using Go `cgo`

`cgo` has a lot of trap.  
but Not "C" pkg also directory in `$GOROOT/src`. IDE's(vim) Goto command not works.  

So, Here collect materials.

cgo compiling file extension
===
## C
`.c`, `.s`, `.S`
## C++
`.cc`, `.cpp`, `.cxx`
## Header
Any `.h`, `.hh`, `.hpp`, `.hxx` files will not be compiled separately.  
but, if these header files are changed, the C and C++ files will be recompiled.

cgo environment variable
===

## Building Go
`CC`, `CXX`, `CC_FOR_TARGET`, `CXX_FOR_TARGET`
## Compiling `.go`
`CGO_CFLAGS`, `CGO_CPPFLAGS`, `CGO_CXXFLAGS`, `CGO_LDFLAGS`

cgo convert C-Go string type
===

## `string`

```go
// Go string to C string; result must be freed with C.free
func C.CString(string) *C.char

// C string to Go string
func C.GoString(*C.char) string

// C string, length to Go string
func C.GoStringN(*C.char, C.int) string

// C pointer, length to Go []byte
func C.GoBytes(unsafe.Pointer, C.int) []byte
```

C Types in Go
===

## `char`
```go
type C.char
type C.schar (signed char)
type C.uchar (unsigned char)
```
## `short`
```go
type C.short
type C.ushort (unsigned short)
```
## `int`
```go
type C.int
type C.uint (unsigned int)
```
## `long`
```go
type C.long
type C.ulong (unsigned long)
```
## `longlong`
```go
type C.longlong (long long)
type C.ulonglong (unsigned long long)
```
## `float`
```go
type C.float  
```
## `double`
```go
type C.double
```

Directly access struct type
===

As in `C.struct_stat`

## `struct`
```
type C.struct_***
```
## `union`
```
type C.union_***
```
## `enum`
```
type C.enum_***
```
## `void*`
See also https://golang.org/pkg/unsafe/
```go
func unsafe.Pointer() *ArbitraryType
```
