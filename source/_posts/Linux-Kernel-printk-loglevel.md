title: '[Linux Kernel] printk loglevel'
date: 2015-07-22 23:10:40
categories: Linux Kernel
tags: Linux Kernel
---
看系統所有由 printk 印出的訊息
`$ dmesg`
or
`$ cat /proc/kmsg`

<!-- more -->

日誌級別定義在 `include/linux/kern_levels.h`，共分 8 個等級

<pre>
#define KERN_EMERG   KERN_SOH "0"     /* system is unusable */
#define KERN_ALERT   KERN_SOH "1"     /* action must be taken immediately */
#define KERN_CRIT    KERN_SOH "2"     /* critical conditions */
#define KERN_ERR     KERN_SOH "3"     /* error conditions */
#define KERN_WARNING KERN_SOH "4"     /* warning conditions */
#define KERN_NOTICE  KERN_SOH "5"     /* normal but significant condition */
#define KERN_INFO    KERN_SOH "6"     /* informational */
#define KERN_DEBUG   KERN_SOH "7"     /* debug-level messages */

#define KERN_DEFAULT   KERN_SOH "d"     /* the default kernel loglevel */
</pre>

printk 可以加上訊息的日誌級別，沒有加的預設為 KERN_DEFAULT，在 `kernel/printk/printk.c` 裡會設定為 4

`printk(KERN_ERR "kernel error message\n");`

## 顯示與控制系統日誌訊息

要知道目前系統的日誌控制訊息可以由這個指令顯示與控制

```bash
$ cat /proc/sys/kernel/printk
3     4     1     3
```

會顯示 4 個數字，分別代表

<pre>
console_loglevel             控制台日誌級別
default_message_loglevel     預設日誌級別，printk 沒有給預設級別的，會以這個為預設
minimum_console_loglevel     console_loglevel 的最高日誌級別限制，console_loglevel 不能超過這個值
default_console_loglevel     console_loglevel 的預設值
</pre>

`console_loglevel = 3` 代表日誌級別在 3 以上的，也就是只有 0，1，2 會印到 console 顯示
`default_message_loglevel = 4` 代表 printk 沒有加上日誌級別的都會當作 4 來處理
`minimum_console_loglevel = 1` 代表 console_loglevel 最大可以設到 1
`default_console_loglevel = 3` 代表 console_loglevel 預設為 3

## Reference
Documentation/sysctl/kernel.txt
