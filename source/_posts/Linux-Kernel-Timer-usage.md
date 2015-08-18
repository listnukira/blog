title: '[Linux Kernel] Timer usage'
date: 2015-08-18 11:15:07
categories: Linux Kernel
tags: Linux Kernel
---
記錄核心計時器(timer)的重點與使用方式

<!-- more -->

計時器的一些重點
* 可以將核心的工作延後到指定的時間後執行
* 只要初始化，指定到期時間，設定到期時要處理的函式與要傳給函式的參數就可以使用
* 到期後會執行指定的函式，並且不會重複執行


###結構

計時器的結構為 `struct timer_list`，被定義在 `include/linux/timer.h`，這裡只列出比較重要的幾個成員

```c include/linux/timer.h
struct timer_list {
        struct hlist_node entry;        /* 計時器串列的項目 */
        unsigned long expires;          /* 到期值，以 jiffies 為單位 */
        void (*function)(unsigned long);/* 到期時會執行的函式 */
        unsigned long data;             /* 傳給到期處理函式的參數 */
};
```

###定義

<pre>
struct timer_list demo_timer
</pre>

###初始化

<pre>
init_timer(&demo_timer)
</pre>

###設定

<pre>
demo_timer.expires = jiffies + delay; /* 計時器在 delay 個週期後到期 */
demo_timer.data = 0;                  /* 將 0 傳給到期處理函式 */
demo_timer.function = demo_function;  /* 設定到期後會處理的函式為 demo_function */
</pre>

###啟用

<pre>
add_timer(&demo_timer);
</pre>

在核心裡 `add_timer()` 會呼叫到 `mod_timer()`，所以其實也可以用 `mod_timer()` 來取代

###修改到期時間

<pre>
mod_timer(&demo_timer, jiffies + new_delay);
</pre>

此函式也可以用在尚未啟用的計時器上，若 `demo_timer` 沒啟用，此函式會啟用它

###刪除

刪除計時器有兩種方式

`del_timer(&demo_timer);`

此函式會刪除已經啟用和還沒啟用的計時器，但是有可能刪除時，計時器已經在另一個處理器上執行了，如果想等正在執行的函式執行結束，要用另一個刪除函式

`del_timer_sync(&demo_timer);`

此函式無法在中斷環境中使用(因為會等待)

因為無法確定計時器的處理函式是不是正在執行，刪除計時器應該優先使用同步版本的 `del_timer_sync()`
在單處理器的系統中，`del_timer_sync()` 會被定義成 `del_timer()`，所以應該使用同步的版本

###注意事項

因為計時器的執行與目前正在執行的程式碼是非同步的，所以有可能會有 race condition 的情況發生，不要用以下的程式碼來代替 `mod_timer()`

<pre>
del_timer(&demo_timer);
demo_timer->expires = jiffies + new_delay;
add_timer(&demo_timer);
</pre>

###範例

這個範例簡單的示範 `timer` 的用法，每隔 `1 2 3 ...` 秒執行 `timer_function` 函式，函式會印出傳進來的參數跟目前的 `jiffies` 值，然後再設定 `timer` 重新執行

`timer_pending()` 函式可以判斷 `timer` 目前是否已被加到佇列中

```c
#include <linux/module.h>
#include <linux/init.h>
#include <linux/timer.h>

static struct timer_list demo_timer;
static unsigned int cnt = 1;

static void timer_function(unsigned long data)
{
        printk("%lu expired jiffies: %lu\n", data, jiffies);

        cnt++;
        demo_timer.data = cnt;
        mod_timer(&demo_timer, jiffies + cnt * HZ);
}

static int __init demo_init(void)
{
        printk("demo_init\n");

        init_timer(&demo_timer);

        demo_timer.expires = jiffies + 1 * HZ;
        demo_timer.data = cnt;
        demo_timer.function = timer_function;

        printk("init jiffies: %lu\n", jiffies);
        add_timer(&demo_timer);

        if (timer_pending(&demo_timer))
                printk("demo_timer pending\n");
        else
                add_timer(&demo_timer); /* never called */

        return 0;
}

static void __exit demo_exit(void)
{
        printk("delete demo_timer\n");
        del_timer_sync(&demo_timer);

        printk("demo_exit\n");
}

module_init(demo_init);
module_exit(demo_exit);

MODULE_LICENSE("Dual BSD/GPL");
```
