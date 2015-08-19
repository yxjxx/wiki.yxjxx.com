---
title: "note for vim advance user"
date: 2015-08-19 12:43
---

# vim advance user

### Lecture 2

```
i: inside
a: around, plus one after space

v: visual
d: delete
y: yank(copy)
c: change

w: word
W: words until space
p: paragraph
s: sentence
t: tag
```

```
viw: entire word
vaw: entire word and one after space

diw
daw

vit
vat

vi( == vib
vi)
vi{ == viB
vi}
vi[
vi]
```



### Lecture 3

```
autocmd event pattern command

syntax on
filetype indent on
set smartindent
autocmd BufRead, BufWritePre *.html normal gg=G "Format html files

"help autocmd-events
set filetype? == set ft?

autocmd Filetype html nnoremap <leader>c I<!--<esc>A--><esc>
autocmd Filetype javascript nnoremap <leader>c I//<esc>

augroup JavaScriptCmds
        autocmd! "使本组 autocmd 失效（It seems not work)
        autocmd Filetype javascript nnoremap <leader>r :!node %<cr>
        autocmd Filetype javascript nnoremap <leader>c I//<esc>
augroup END
```



### Lecture 4

```
:set number
:set nonumber
:set number!
:set number?
:set relativenumber
:set background=dark/light
:set background
:set bg?
:set wrap
:set nowrap
:setlocal wrap
:setl wrap
```



### Lecture 5

```
:map

:set textwidth=50
:set numberwidth=3
:set linebreak
:set nolinebreak
:set showbreak='> '

let mapleader=','
noremap <left> <nop>
noremap <up> <nop>

:w foo2
:saveas foo2
```

### Lecture 6

```
 :set scrolloff=5
 :set showmode
 :set noshowmode
 :set wildmenu
 :set wildmode=full
 :set cursorline
 :set undofile
 :set gdefault
```

### Lecture 7

**clipborad**

```
:reg

 default register ""

 ""add: delete the line and copy it into register "a
 "ap : paste the content in "a register

 anything you yank will also go to "0

 "q
 @q record your motions
```

### Lecture 8

**Insert mode**

```
<c-h>: backspace
<c-w>: delete a word before the cursor
<c-u>: delete the words to the beginning of the line before the cursor
<c-v>[anykey]: inset [anykey]'s vim key code e.g.: ^M for enter, ^[ for ESC
<c-o>: temporaily to cmd mode. e.g.: <c-o>j go down oneline and still in insert mode
<c-r>[anyreg]: paste the content of [anyreg]. e.g.: <c-r>q
<c-r>=: execute any vimscript. e.g.: <c-r>=7*52 it will paste 364 into where the cursor was.
```

### Lecture 9

**map**



```
:re means: recursive
:map
:nmap x dd "normal map x to dd
:nmap z x  "normal map z to x, but z will be recursivly mapped to dd

:nnoremap x dd
:nnoremap z x  :x will delete a whole line, z will delete one character.

In every mode of vim, there is a map method

noremap
nnoremap
inoremap
vnoremap
onoremap

autocmd Filetype javascript nnoremap <buffer> <leader>c I//<esc> "this map only works under current buff

:onoremap p i(    e.g.: ci( == cp

```

### Lecture 10

**regular expression search**

```
set hlsearch
set incsearch

:help magic
nnoremap / /\v "Use reg search
vnoremap / /\v
nnoremap ? ?\v
nnoremap ? ?\v

nnoremap <leader><space> :noh  "no highlight

Search first and substitue
/\vone  "all one is highlight
:%s//WON/ "vim will replace all the highlighted one with WON
```

### Lecture 11

```
gj
gk
g0
g$
nnoremap j gj

gf "open the file under the cursor

:bd! "delete the current buffer

J "join the next line, seperated with space
K "man page for the word under current cursor
:help K

zz "move current line to the middle of the screen

visual mode
o "toggle cursor between the corner of the block
O "between the same line corner

. "repeat last action
fs ; , * # %
```

### Lecture 12

**vim function**

```
function! AddHelloToTop()
    normal HOhello there^[A vim user^[ "^[ represent for ESC use <c-v>Esc to get it.
    s/hello there/hi/
    return "we add a message"
endfunction

:call AddHelloToTop()

command! Hello call AddHelloToTop()

:Hello

nnoremap <leader>h :call AddHelloToTop()<cr> "<cr> hit enter

:echom AddHelloToTop() "echom add the message to messages list
:messages  "show all the messages



```

### Lecture 13

**auto completion**

```
<c-n>
<c-p>

function! InsertTabWrapper()
    let col = col(".") - 1
    if !col || getline(".")[col - 1] !~ '\k'
        return "\<tab>"
    else
        return "\<c-n>"
 endfunction

 inoremap <tab> <c-r>=InsertTabWrapper()<cr>
 inoremap <s-tab> <c-p>
```

### Lecture 14

**different filetype specific setting**

```
~/.vim/ftplugin/javascript.vim

you need filetype plugin indent on in .vimrc
```

### Lecture 15

**abbreviations**

```
:abbrev teh the  "自动纠正 teh 为 the，适用于有一些经常打错的词

inoreabbrev teh the
inoreabbrev fu function
cnoreabbrev Wq wq
cnoreabbrev WQ wq
cnoreabbrev wrap set wrap
cnoreabbrev nowrap set nowrap
```

### Lecture 16

**statusline**

```
:help statusline
```

### Lecture 17

**find plugin for your language**

e.g.: coffeescript

### Lecture 18

**Plugin: vim.surroud**

```
快速增减括号,引号之类的包围符号.

cs"'  "替换双引号为单引号
cst"  "替换包围符为双引号
ds"   "删除包围符"
ysiw] "在光标下的单词周围加上[]包围符.  iw是一个文本对象，即光标下的单词.
yss yS ySS 整行操作.
在包围符号为括时，输入左括号(或者{,则会留一个空格.
```

### Lecture 19

**Plugin: snipmate**

### Lecture 20

**janus** vim distrbution

```
if filereadable(expand("~/.vimrc.before"))
    source ~/.vimrc.before
 endif

```

