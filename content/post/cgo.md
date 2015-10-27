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

Compiler flags
===

## flags
Several important flag:

```bash
-h help
-S print assembly listing
-m print optimization decisions such as escape analysis
-l turn off inlining, repeat to make inlining more aggressive
-N disable optimizations
-B disable bounds checking
```
Usage: 

```bash
go build -gcflags=-S pkg
go tool compile -S a.go b.go c.go
```

## GODEBUG
Useful GODEBUG variables for performance:

```bash
allocfreetrace=1: print all allocs and frees (it's a lot!)
gctrace=1, gctrace=2: print GC activity
schedtrace=X: print scheduler state every X ms
scheddetail=1: print detailed scheduler state
```

## GCGC
GOGC variabels:

```
GOGC=off go run x.go
# Or
runtime.SetGCPercent(-1) // -1 for off, 50 for aggressive GC, 100 for default, 200 for lazy GC
```

Usage:

```bash
GODEBUG=scheddetail=1,schedtrace=1000 go run x.go
```

## ldflags

Traditional build:
```bash
go build helloworld.go && stat -f "%N: %z bytes" helloworld
helloworld: 2344944 bytes
```

Without DWARF:
```
go build -ldflags=-w helloworld.go && stat -f "%N: %z bytes" helloworld
helloworld: 1746928 bytes
```
But you lose debug information.

## See also
- Go Performance Tutorial on PayPal / http://cdn.oreillystatic.com/en/assets/1/event/129/Go%20performance%20tutorial%20Presentation%201.pdf
- Cgo の基本的な使い方とポインタ周りのTips / http://r9y9.github.io/blog/2014/03/22/cgo-tips/
- cgoでGolangとC++ライブラリをリンクするとき、何が起きているのか / https://beatsync.net/main/log20141022.html
- Why my Go program is slow? / http://www.slideshare.net/InadaNaoki/gocon2014-pprof
- よくみる extern "C" {} と __cplusplus / http://hakobe932.hatenablog.com/entry/20090104/1231073299
