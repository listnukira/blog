title: '[C/C++] 判斷 endianness'
date: 2015-08-14 23:16:59
categories: C/C++
tags: C/C++
toc: false
---
一個判斷 Endian 的函式

<!-- more -->

`Big Endian`
資料從 MSB 開始放到最低的記憶體位址上

`Little Endian`
資料從 LSB 開始放到最低的記憶體位址上 


這個函式是在 module-init-tools 裡看到的

```c util.c
int endianness()
{
    return (char) *((unsigned int*)("\1\0\0\2"));
}
```

`("\1\0\0\2")` 在記憶體中的位址由低到高為 `01 00 00 02`，如果由整數指標來表示的話

Big Endian    會是 `0x01000002`
Little Endian 會是 `0x02000001`

之後再由 char 來取 LSB 的值回傳，回傳 1 代表 Little Endian，2 代表 Big Endian

