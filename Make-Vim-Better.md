---
title: Make Vim Better
data: 30-07-2021
---
Finding files:
nnoremap ,f :find *
nnoremap ,F :find <C-R>=expand('%:p:h').'/**/*'<CR>
nnoremap ,s :sfind *
nnoremap ,S :sfind <C-R>=expand('%:p:h').'/**/*'<CR>
nnoremap ,v :vert sfind *
nnoremap ,V :vert sfind <C-R>=expand('%:p:h').'/**/*'<CR>
Line bubbling:
nnoremap ,<Up>   :<C-u>silent! move-2<CR>==
nnoremap ,<Down> :<C-u>silent! move+<CR>==
xnoremap ,<Up>   :<C-u>silent! '<,'>move-2<CR>gv=gv
xnoremap ,<Down> :<C-u>silent! '<,'>move'>+<CR>gv=gv
Word bubbling:
nnoremap ,<Left>  "_yiw?\v\w+\_W+%#<CR>:s/\v(%#\w+)(\_W+)(\w+)/\3\2\1/<CR><C-o><C-l>
nnoremap ,<Right> "_yiw:s/\v(%#\w+)(\_W+)(\w+)/\3\2\1/<CR><C-o>/\v\w+\_W+<CR><C-l>
Insert mode completion:
inoremap ,, <C-x><C-o><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
inoremap ,; <C-n><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
inoremap ,: <C-x><C-f><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
inoremap ,= <C-x><C-l><C-r>=pumvisible() ? "\<lt>Down>\<lt>C-p>\<lt>Down>" : ""<CR>
Include search:
nnoremap ,I :Ilist<Space>
Grepping (with ag):
nnoremap <silent> ,G :Grep <C-r><C-w><CR>
xnoremap <silent> ,G :<C-u>let cmd = "Grep " . functions#GetVisualSelection() <bar>
                        \ call histadd("cmd",cmd) <bar>
Quick search/replace:
nnoremap <Space><Space> :'{,'}s/\<<C-r>=expand('<cword>')<CR>\>/
xnoremap <Space><Space> :<C-u>'{,'}s/<C-r>=functions#GetVisualSelection()<CR>/
Quick repeat:
nnoremap ,; *``cgn
nnoremap ,, #``cgN
xnoremap ,; <Esc>:let @/ = functions#GetVisualSelection()<CR>cgn
xnoremap ,, <Esc>:let @/ = functions#GetVisualSelection()<CR>cgN
Go to definition:
nnoremap ,t :Bombit<CR>:tjump /
nnoremap ,p :Bombit<CR>:ptjump /
nnoremap ,D :Dlist<Space>
Increment a column of numbers:
xnoremap <silent> ,i :<C-u>let vcount = v:count<CR>gv:call functions#Incr(vcount)<CR>
Actual delete:
nnoremap ,d "_d
xnoremap ,d "_d
Actual "paste over":
xnoremap ,p "_dP
Isolate current line:
nnoremap ,<Space><Space> m`o<Esc>kO<Esc>``
List available snipmate completions:
imap ,<Tab> <C-r><Tab>
(JS) Banner-like comment:
nnoremap <buffer> ,g I// <Esc>A //<Esc>yyp0llv$hhhr-yykPjj
(JS) console.log mappings:
nnoremap <buffer> ,l yiwoconsole.log("<C-r>"", <C-r>");<Esc>
xnoremap <buffer> ,l yoconsole.log("<C-r>"",<C-r>");<Esc>
nnoremap <buffer> ,q ciw"<C-r>"", <C-r>"<Esc>
xnoremap <buffer> ,q c"<C-r>"", <C-r>"<Esc>
And a few "experimental" ones…
Quick :global:
nmap ,# :g/<C-r><C-w>/#<CR>
nmap ,@ :g//#<Left><Left>
Specialized (and broken) search/replace:
nnoremap <Space>f "zyiwm'/{<CR>%V'':s/\<<C-r>z\>/
nnoremap <Space>b "zyiwVi(:s/\<<C-r>z\>/
nnoremap <Space>B "zyiwVi{:s/\<<C-r>z\>/
