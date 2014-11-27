title: "[C/C++] 結構裡的冒號 - Bit Fields"
date: 2014-11-26 13:56:29
categories: C/C++
tags:
- C/C++
---
在結構裡的冒號稱為 Bit Field，可以用來節省記憶體空間

<!-- more -->

## Bit Field

宣告方式如下

``` c
struct {
    type [member_name] : width;
    unsigned char c : 3;
}
```

width 代表會用到 type 的多少 bit，不能超過 type 所代表的位元數，以上面的 `unsigned char c : 3` 來說，`char` 用 8 bits 來表示，而 width 等於 3，表示只會用到前三個 bit

### 範例 1

這個範例用來表示使用/不使用 Bit Fields 的情況下，結構在記憶體中所佔的大小

``` c
#include <stdio.h>
#include <string.h>

/* define simple structure */
struct {
    unsigned int a;
    unsigned int b;
} status1;

/* define a structure with bit fields */
struct {
    unsigned int a : 1;
    unsigned int b : 3;
} status2;
 
int main()
{
    printf("Memory size occupied by status1 : %d\n", sizeof(status1)); // 8
    printf("Memory size occupied by status2 : %d\n", sizeof(status2)); // 4

    struct status2 s;
    s.b = 7;
    s.b = 8; // error!

   return 0;
}
```

### 範例 2

``` c
struct status1 {
    char a : 3;
    int b : 29;
};
// sizeof(struct status1) = 4

struct status2 {
    char a : 4;
    int b : 29;
};
// sizeof(struct status2) = 8
```

## Reference
http://www.tutorialspoint.com/cprogramming/c_bit_fields.htm
