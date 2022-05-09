---
title: Make Vim Better
date: 30-07-2021
private: false
---

Finding files:
```vim
nnoremap ,f :find *
```
```vim
nnoremap ,F :find <C-R>=expand('%:p:h').'/**/*'<CR>
```
```
nnoremap ,s :sfind *
```
```vim
nnoremap ,S :sfind <C-R>=expand('%:p:h').'/**/*'<CR>
```
```vim
nnoremap ,v :vert sfind *
```
```vim
nnoremap ,V :vert sfind <C-R>=expand('%:p:h').'/**/*'<CR>
```
Line bubbling:
```vim
nnoremap ,<Up>   :<C-u>silent! move-2<CR>==
```
```vim
nnoremap ,<Down> :<C-u>silent! move+<CR>==
```
```vim
xnoremap ,<Up>   :<C-u>silent! '<,'>move-2<CR>gv=gv
```
```vim
xnoremap ,<Down> :<C-u>silent! '<,'>move'>+<CR>gv=gv
```
Word bubbling:

```vim
nnoremap ,<Left>  "_yiw?\v\w+\_W+%#<CR>:s/\v(%#\w+)(\_W+)
```
```vim
(\w+)/\3\2\1/<CR><C-o><C-l>
```
```vim
nnoremap ,<Right> "_yiw:s/\v(%#\w+)(\_W+)(\w+)/\3\2\1/<CR><C-
o>/\v\w+\_W+<CR><C-l>
```
```vim
Insert mode completion:
```vim
inoremap ,, <C-x><C-o><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
```
```vim
inoremap ,; <C-n><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
```
```vim
inoremap ,: <C-x><C-f><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
```
```vim
inoremap ,= <C-x><C-l><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
```
Include search:
```vim
nnoremap ,I :Ilist<Space>
```
Grepping (with ag):
```vim
nnoremap <silent> ,G :Grep <C-r><C-w><CR>
```
```vim
xnoremap <silent> ,G :<C-u>let cmd = "Grep " . 
functions#GetVisualSelection() <bar>
                        \ call histadd("cmd",cmd) <bar>
```
Quick search/replace:
```vim
nnoremap <Space><Space> :'{,'}s/\<<C-r>=expand('<cword>')<CR>\>/
```
```vim
xnoremap <Space><Space> :<C-u>'{,'}s/<C-r>=functions#GetVisualSelection()<CR>/
```
Quick repeat:
```vim
nnoremap ,; *``cgn
```
```vim
nnoremap ,, #``cgN
```
```vim
xnoremap ,; <Esc>:let @/ = functions#GetVisualSelection()<CR>cgn
```
```vim
xnoremap ,, <Esc>:let @/ = functions#GetVisualSelection()<CR>cgN
```
Go to definition:
```vim
nnoremap ,t :Bombit<CR>:tjump /
```
```vim
nnoremap ,p :Bombit<CR>:ptjump /
```
```vim
nnoremap ,D :Dlist<Space>
```
Increment a column of numbers:
```vim
xnoremap <silent> ,i :<C-u>let vcount = v:count<CR>gv:call functions#Incr(vcount)<CR>
```
Actual delete:
```vim
nnoremap ,d "_d
```
```vim
xnoremap ,d "_d
```
Actual "paste over":
```vim
xnoremap ,p "_dP
```
Isolate current line:
```vim
nnoremap ,<Space><Space> m`o<Esc>kO<Esc>``
```
List available snipmate completions:
```vim
imap ,<Tab> <C-r><Tab>
```
(JS) Banner-like comment:
```vim
nnoremap <buffer> ,g I// <Esc>A //<Esc>yyp0llv$hhhr-yykPjj
```
(JS) console.log mappings:
```vim
nnoremap <buffer> ,l yiwoconsole.log("<C-r>"", <C-r>");<Esc>
```
```vim
xnoremap <buffer> ,l yoconsole.log("<C-r>"",<C-r>");<Esc>
```
```vim
nnoremap <buffer> ,q ciw"<C-r>"", <C-r>"<Esc>
```
```vim
xnoremap <buffer> ,q c"<C-r>"", <C-r>"<Esc>
```
And a few "experimental" ones…
Quick :global:
```vim
nmap ,# :g/<C-r><C-w>/#<CR>
```
```vim
nmap ,@ :g//#<Left><Left>
```
Specialized (and broken) search/replace:
```vim
nnoremap <Space>f "zyiwm'/{<CR>%V'':s/\<<C-r>z\>/
```
```vim
nnoremap <Space>b "zyiwVi(:s/\<<C-r>z\>/
```
```vim
nnoremap <Space>B "zyiwVi{:s/\<<C-r>z\>/
```

