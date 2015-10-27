+++
categories = ["golang"]
date = "2015-10-26T10:29:36+09:00"
title = "dispatch"

+++

OS Xのnativeスレッド管理のGrand Central DispatchをGoにバインドするべく，がんばっている． 
ただexec.Command("echo hello")をdispatchでrunすることはできたけど，APIとしてなんらかのGo funcを  
dispatchに埋め込む方法がまだ分からない．

Goでのclojure call funcが解決の糸口？

そもそも，AppleがCを拡張して実装したBlockをGoで表現できれば解決するのだけど．．．

または
https://github.com/aventurella/go-xpc
でもdispatchを使っているので，参考にしたい．

