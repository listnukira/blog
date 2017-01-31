title: '[Vim] Plugin'
date: 2016-04-20 00:07:10
categories: Vim
tags: Vim
---
紀錄目前有在使用的 vim plugin 和一些設定，plugin 都以有在 GitHub 上的 repo 為主

<!-- more -->

## VundleVim/Vundle.vim

管理 vim plugin 的工具，新增與移除都很方便

## tmux-plugins/vim-tmux

給 Tmux 用的，讓 `.tmux.conf` 有更好的語法高亮

## altercation/vim-colors-solarized

vim 的配色

<pre>
colorscheme solarized
set background=dark
</pre>

## nacitar/a.vim

快速的在 .h 檔與 .c 檔之間切換，檔案名稱要一樣，也要在相同資料夾內

設定成按 `<leader>a` 就可快速切換

<pre>
nmap <leader>a :A<CR>
</pre>

## easymotion/vim-easymotion

快速的在文字間移動，目前比較常用到的是

`<leader>w`，在 word 間移動
`<leader>s`，輸入兩個字母移動
`<leader>j`，往下移動
`<leader>k`，往上移動

<pre>
let g:EasyMotion_do_mapping=0
map &#60;leader&#62; &#60;Plug&#62;(easymotion-prefix)

nmap &#60;leader&#62;s &#60;Plug&#62;(easymotion-s)
nmap &#60;leader&#62;s &#60;Plug&#62;(easymotion-s2)

map &#60;leader&#62;w &#60;Plug&#62;(easymotion-bd-w)
map &#60;leader&#62;j &#60;Plug&#62;(easymotion-j)
map &#60;leader&#62;k &#60;Plug&#62;(easymotion-k)
</pre>

## scrooloose/nerdcommenter

快速註解程式碼

`<leader>c<space>`，註解或取消註解一行或一個區塊，原本有註解就取消，沒有就新增

預設的是用 `/* */` 來註解，即使多行註解也是每行加上 `/**/`，修改成使用 `//` 的方式
<pre>
let g:NERDCustomDelimiters = {
    \ 'c': { 'left': '//', 'leftAlt': '/*', 'rightAlt': '*/'}
    \ }
</pre>

在處理多層註解時，如果原本就有 `/**/` 的註解，再註解一次的話會變成 `[> <]`，看文件是說取消註解就會變回來，自己測試卻不會變回來，所以把設定關掉
<pre>
let g:NERDUsePlaceHolders=0
</pre>

## tpope/vim-surround

快速新增/刪除/修改成對的符號，像是各種括號，單引號，雙引號

`cs'"`，把 ' 換成 "
`ds'`，把 ' 刪除
`ysiw'`，新增 ' 到字的前後
`ysiW'`，新增 ' 到整串字的前後
`ysw'`，新增 ' 到字的前後，以目前游標開始
`ysW'`，新增 ' 到整串字的前後，以目前游標開始

如果新增/修改的符號是括號類的 (大中小括號)，左括號代表會多一格空白，右括號沒有空白

## Valloric/MatchTagAlways

Highlight 對應的標籤，因為考慮到效能，只有在同一頁的標籤才會被 highlight

## kshenoy/vim-signature

新增／刪除 mark

`m,`，標記一個可用的 mark
`m-`，刪除目前這行的 mark
`m<space>`，刪除所有 mark
`']`，依照字母順序跳到下一個 mark

## vim-scripts/matchit.zip

擴充原本的 % 功能到 HTML, XML, LaTex 之類的檔案

## vim-scripts/AutoClose--Alves

自動補齊括號，單引號，雙引號，另外加上兩行設定方便使用

<pre>
inoremap {<CR> {<CR>}<ESC>O
inoremap &#123;&#123; {
</pre>

第一個設定在寫函式或者程式區塊時，打左大括號再按 Enter 會自動補齊並跳到區塊裡等待輸入
第二個設定是連按兩次左大括號代表不要補齊
