title: '[Linux Kernel] pr_debug display'
date: 2015-08-13 11:16:15
categories: Linux Kernel
tags: Linux Kernel
toc: false
---

`pr_debug` 在編譯的時候如果沒特別指定參數，預設會是一個空巨集，所以不會印東西出來

<!-- more -->

根據 `include/linux/printk.h` 裡的定義

```c include/linux/printk.h
#if defined(CONFIG_DYNAMIC_DEBUG)
#define pr_debug(fmt, ...) \
        dynamic_pr_debug(fmt, ##__VA_ARGS__)
#elif defined(DEBUG)
#define pr_debug(fmt, ...) \
        printk(KERN_DEBUG pr_fmt(fmt), ##__VA_ARGS__)
#else
#define pr_debug(fmt, ...) \
        no_printk(KERN_DEBUG pr_fmt(fmt), ##__VA_ARGS__)
#endif
```

在編譯的時候 `Makefile` 要加上 `CFLAGS_[module_name].o := -DDEBUG`

