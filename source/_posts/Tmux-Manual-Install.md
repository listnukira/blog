title: '[Tmux] Manual Install'
date: 2017-01-31 21:51:12
categories: Tmux
tags: Tmux
---

紀錄安裝 Tmux 的步驟

<!-- more -->

Tmux 編譯需要 libevent，而 libevent 需要 ncurses，如果不知道主機上有沒有裝這兩個 library，可以都裝在自己的 local 目錄，不然也可以先嘗試編譯 Tmux，configure 時如果有缺會報錯，這時就要自己編譯 libevent，同樣也是可以先編譯看看，有缺再裝 ncurses

### Version
ncurses: 5.9
libevent: 2.1.8-stable
tmux: master, 9b9a5a292d

### ncurses
``` bash
wget http://invisible-island.net/datafiles/release/ncurses.tar.gz
tar xvzf ncurses.tar.gz
cd ncurses-*
./configure --prefix=/home/${USER}/local
make
make install
```

### libevent
``` bash
wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
cd libevent-2.1.8-stable
./configure --prefix=/home/${USER}/local
make
make install
```

### Tmux
``` bash
git clone https://github.com/tmux/tmux
cd tmux
./autogen.sh

./configure --prefix=/home/${USER}/local LIBEVENT_CFLAGS="-I/home/${USER}/local/include" LIBEVENT_LIBS="-L/home/${USER}/local/lib -levent"
or
CFLAGS="-I/home/${USER}/local/include" LDFLAGS="-L/home/${USER}/local/lib" ./configure --prefix=/home/${USER}/local

make
make install
```

### Environment Variables
``` bash
export PATH="/home/${USER}/local/bin:${PATH}"
export LD_LIBRARY_PATH=/home/${USER}/local/lib
```

