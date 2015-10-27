+++
categories = ["golang"]
date = "2015-10-16T19:20:55+09:00"
title = "go cgo"

+++

Goのcgo実装について

## 主な実装内容
ここが詳しい
http://akrennmair.github.io/golang-cgo-slides/

### CからGoのコードを呼ぶ
http://akrennmair.github.io/golang-cgo-slides/#9

Goのfuncの上に//exportを記述することによって，上部記述したCのコードからGoを呼べるようになる
`extern void hogehoge`については，Cを勉強する．．．

### Mapping the C namespace to Go
Everything declared in the C code is available in the C pseudo-package
Fundamental C data types have their counterpart,
```
int → C.int
unsigned short → C.ushort
```
The Go equivalent to `void * is unsafe.Pointer`
typedefs are available under their own name
structs are available with a struct_ prefix, 
```
struct foo → C.struct_foo
```
same goes for unions and enums

だそう．
