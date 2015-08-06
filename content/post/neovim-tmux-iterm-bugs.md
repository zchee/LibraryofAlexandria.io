+++
date = "2015-07-19T05:43:41+09:00"
title = "neovim tmux iterm bugs"

+++

# 前提
iTerm2 Night（2015-07-19 8:37 AM）上でtmux 2.0あるいはHEAD buildを起動し、neovimを使っている状態。  
neovimのthird-partyはHEADにしてセルフビルドしてる。

# Neovim

## 矢印キーの連続入力で、^[OA、^[OB、^[OC、^[ODがまれに入力、またはinsertモードに切り替わる
neovim独自のもよう。vimではしっかりとは検証してない。  
何しろこれの改善に2週間ほど費やしたからだ！ろくにコードなんて書けたもんじゃない。  
他の人はなぜ苦労していないのか。issueがほとんど見当たらない。  

ちなみにhjklでえぇやんという話なのだけど、Dvorak使いなのでそもそもhjklが横並びではないのと、Kinesis Advantageなので割と矢印キーが押しやすい位置にあるため。  
Dvorakのdhtnにhjklを割り当ててることも考えたけど、dとnの場所に慣れてしまってたのでそれもなぁという感じ。

だけどVimを諦めるわけにはいかないし、今さらIntellijに戻るのもvimに入門したのがもったいない。  
100%の再現性ではなくて、まれに起きる。  ただ、ncursesのマップ上`<Left>`が^[ODなので、どこかの行でずっと`<Left>`を押せば確認可能。その行が`dd`したように削除される。  
なんだけどこれもかなり押してないとでない時もある。  
あとは`<C-S-v>`のVisual blockで再現性が高い。

neovimのlibtermkey、tmuxのterminal-overridesなど、iTermの実装、Karabinerのキーリピートのオーバーライド、どれが原因かまだ判明しない…  
たぶんKarabinerのキーリピート最速設定のせいでneovimがキーを拾う際に追いつかない感じ  
詳しくはvimのhelpでわかる  
// TODO vim helpのキーワードを思い出す

~~ただ今現状直っているので、~~直ってなかった。今の環境と関連しそうな設定ファイルを載せておく

- ARCH: amd64
- OS: darwin
- OS Version: OS X 10.11 El Capitan Beta3 build 15A216g
  - Yosemite 10.10.4でも確認
- Keyboard: Kinesis Advantage
  - MacBook Proのベンダーキーボードでも確認

```vim
nvimrc
```

```conf
tmux.conf
```

```plist
com.googlecode.iterm2.plist
```

```plist
Karabiner settings
```

## 試行錯誤の履歴たち

### `set nocompatible`
vimでは有効だが、neovimはそもそもデフォルトで有効になっているらしく、nvimrcにあっても無視される  
// TODO neovimのnocompatibleあたりのソースコードのURL

### よく言われる、`<xLeft>`にkeycode escaepe sequenceをnnoremapしてtimeoutlenを200程度に

```vim
" http://superuser.com/questions/401926/how-to-get-shiftarrows-and-ctrlarrows-working-in-vim-in-tmux
if $TERM =~ '^xterm'
  " tmux will send xterm-style keys when its xterm-keys option is on
  execute "set <Up>=\Eku"
  execute "set <Down>=\Ekd"
  execute "set <Right>=\Ekr"
  execute "set <Left>=\Ekl"
  execute "set <xUp>=\Eku"
  execute "set <xDown>=\Ekd"
  execute "set <xRight>=\Ekr"
  execute "set <xLeft>=\Ekl"
endif
if $TERM =~ '^screen'
  " tmux will send xterm-style keys when its xterm-keys option is on
  execute "set <xUp>=\e[1;*A"
  execute "set <xDown>=\e[1;*B"
  execute "set <xRight>=\e[1;*C"
  execute "set <xLeft>=\e[1;*D"
endif
```

人間が入力できる限界値を超えたtimeoutlenを設定して防ぐ方法だけど、Karabinerのキーリピート最速設定には勝てない  
が原因だと、現状は判断してる。

### nvimrcで`<Left>`などをhにnnoremap

```vim
" http://vim.wikia.com/wiki/Fix_arrow_keys_that_display_A_B_C_D_on_remote_shell
noremap <silent> <Up> <Nop>
noremap <silent> <Down> <Nop>
noremap <silent> <Right> <Nop>
noremap <silent> <Left> <Nop>
nnoremap <silent> <Up>    <Nop>
nnoremap <silent> <Down>  <Nop>
nnoremap <silent> <Right> <Nop>
nnoremap <silent> <Left>  <Nop>
nnoremap <silent> <Left>  h
nnoremap <silent> <Down>  j
nnoremap <silent> <Up>    k
nnoremap <silent> <Right> l
```

同じくKarabinerのキーリピート速度にtimeoutlenが勝てない  
さらにはnoremapやmapだとinsertモードでカーソル使えなくなる  
insert対策として  
`inoremap <Left> <C-o><Left>`  
をやると、deoplete、YouCompleteMeやOmnifuncが誤作動する。移動するたびに補完が効いて決定され、文字が勝手に入力されていく  
…そのうえそもそも改善しない

### infocmpでxterm-256colorのterminfoを取得してkcab1などを書き換え、ticで再コンパイル、`export TERMINFO=~/.terminfo`
zsh側でbackward-char,forward-char,upline-or-history,downline-or-historyなどのの設定が必要なうえ、lessなどにはzshの設定は効かず、pecoにはそのままODなどとと入力され、しかも改善しない

### tmux.confのterminal-overridesでkcub1=\Eklなど
zsh側で（ｒｙ  
さらにはこれだと今までよりも頻繁に起きるようになる  
このタイミングでKarabinerの設定を遅くしたことが原因かもしれない

## nvimrc2行目に`scriptencoding 'utf-8'` が設定されていると、日本語入力が文字化けする
neovimのみの挙動か、nvimrcの記述の順番によるもの、あるいはプラグインによるものか未調査。

# tmux
のちほど

# iTerm
のちほど
