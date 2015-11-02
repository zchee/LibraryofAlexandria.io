+++
categories = ["bookmark"]
date = "2015-07-19T17:29:26+09:00"
title = "vim bookmark"

+++

termcap optionsの一覧が見れて便利  

```vim
:help termcap-options
```

現在のsyntaxの名前をecho  
超便利  
~/.nvim/after/syntax/vim.vimとかいじるのに便利

```
:echo synIDattr(synID(line("."), col("."), 1), "name")
```

quickfixのerrorformatの記述方法は、以下を参照

```
http://vim-jp.org/vimdoc-ja/quickfix.html#error-file-format
```
