title: '[Vim] Solarized color theme'
date: 2015-08-05 23:44:09
categories: Vim
tags:
- Vim
- Solarized
---

記錄配色換到 Solarized 的一些注意事項

<!-- more -->

原本的配色是 [seoul256](https://github.com/junegunn/seoul256.vim)，最近換成 [solarized](http://ethanschoonover.com/solarized) 的配色，紀錄我做過的動作

##Putty 設定

因為平常都是用 putty 來連到遠端的設備，根據[官方](http://ethanschoonover.com/solarized/vim-colors-solarized)的說法，必須將 putty 配色也改成 Solarized 的，如果不想更改 putty 的配色也可以，有提供選項 `let g:solarized_termcolors=256` 支援，但效果很差，不如不換...

從官方網站下載配色的壓縮檔 [Solarized.zip](http://ethanschoonover.com/solarized/files/solarized.zip)，解壓縮後進到 `putty-colors-solarized` 資料夾，編輯 `solarized_dark.reg`，將第 3 行最後的 `Solarized%20Dark` 換成想更改配色的 Session，改好後執行，接著重啟 Session 應該就會套用新的配色

##Bash/Dircolors 設定

改了 putty 的配色後，執行 `ls` 會發現不同檔案類型的顏色差異變得很不清楚，目前參考 [Better dircolors with Solarized](http://archlinux.me/w0ng/2012/04/21/better-dircolors-with-solarized/) 的做法，在家目錄下放修改過後的 [dircolors](https://github.com/listnukira/dot-files/blob/master/dircolors)，然後在 `bashrc` 加上

`test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"`

這行指令會修改環境變數 `LS_COLORS` 的設定

##Vim 設定

因為目前用 [Vundle](https://github.com/VundleVim/Vundle.vim) 來管理套件，所以 vimrc 裡要加上

`Plugin 'altercation/vim-colors-solarized'`

vimrc 的其它設定

<pre>
colorscheme solarized
set background=dark
</pre>

因為有用到 mark 的功能，左邊的 gutter 顏色也會跑掉，參考[這裡](http://stackoverflow.com/questions/15277241/changing-vim-gutter-color)，新增以下設定

`highlight clear SignColumn`

##Tmux 設定

Tmux 也有關於 Solarized 的配色，將[設定檔](https://github.com/seebi/tmux-colors-solarized/blob/master/tmuxcolors-dark.conf)加入 tmux.conf 就完成了

