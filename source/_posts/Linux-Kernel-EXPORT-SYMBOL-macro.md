title: "[Linux Kernel] EXPORT_SYMBOL macro"
date: 2014-10-30 15:11:42
categories: Linux Kernel
tags:
- Linux Kernel
---
在 Linux 核心原始碼裡面，到處都可以看到 EXPORT_SYMBOL 系列的巨集，這些巨集用來匯出核心裡的符號，功能與 extern 很類似，但是應用卻不太一樣，由 extern 匯出的符號是供核心靜態編譯所使用，而 EXPORT_SYMBOL 匯出的符號可以給其它模組使用

對於 Linux 核心而言，所有的符號引用都會在靜態連結的階段完成，而一個動態載入的模組可能會需要用到核心裡的函式，因此會需要 EXPORT_SYMBOL 巨集的幫助，由 EXPORT_SYMBOL 匯出的符號會統一放在一個 section，載入模組時如果有未解析的符號就會到這個 section 裡找

## EXPORT_SYMBOL

EXPORT_SYMBOL 系列巨集有下面幾種
<pre>
EXPORT_SYMBOL()            匯出給任何的 module 使用
EXPORT_SYMBOL_GPL()        匯出給有 GPL-licensed 的 module 使用
EXPORT_SYMBOL_GPL_FUTURE() 現在所有 module 都能使用，但是以後只給 GPL-licensed 的 module 使用
EXPORT_UNUSED_SYMBOL()     以後將不再匯出這個符號，應該盡量避免使用
EXPORT_UNUSED_SYMBOL_GPL() 以後將不再匯出這個符號，應該盡量避免使用
</pre>

以 EXPORT_SYMOL 巨集來介紹，EXPORT_SYMOL 巨集定義在 `include/linux/export.h`

``` c include/linux/export.h
/* For every exported symbol, place a struct in the __ksymtab section */
#define __EXPORT_SYMBOL(sym, sec)               \
    extern typeof(sym) sym;                 \
    __CRC_SYMBOL(sym, sec)                  \
    static const char __kstrtab_##sym[]         \
    __attribute__((section("__ksymtab_strings"), aligned(1))) \
    = VMLINUX_SYMBOL_STR(sym);              \
    extern const struct kernel_symbol __ksymtab_##sym;  \
    __visible const struct kernel_symbol __ksymtab_##sym    \
    __used                          \
    __attribute__((section("___ksymtab" sec "+" #sym), unused)) \
    = { (unsigned long)&sym, __kstrtab_##sym }

#define EXPORT_SYMBOL(sym)                  \
    __EXPORT_SYMBOL(sym, "")
```

第 4 行的 `__CRC_SYMBOL(sym, sec)` 是核心做版本控制所使用的，這裡先忽略
將 EXPORT_SYMBOL(sym) 中的 sym 用 my_funciton 代入，並且展開巨集之後會變成

``` c
extern typeof(myfunction) myfunction;

__CRC_SYMBOL(myfunction, "")

static const char __kstrtab_myfunction[]
    __attribute__((section("__ksymtab_strings"), aligned(1)))
    = VMLINUX_SYMBOL_STR(myfunction);

extern const struct kernel_symbol __ksymtab_myfunction;

const struct kernel_symbol __ksymtab_myfunction
    __attribute__((section("___ksymtab+myfunction"), unused))
    = { (unsigned long)&myfunction, __kstrtab_myfunction }
```

從上面的程式碼可以看出 EXPORT_SYMBOL 巨集會定義兩個變數，第一個變數是第 5 行的 `__kstrtab_myfunction`，是一個 char 指標，指向 `VMLINUX_SYMBOL_STR(myfunction)` 返回的字串，`VMLINUX_SYMBOL_STR` 定義為

``` c include/linux/export.h
/* Some toolchains use a `_' prefix for all user symbols. */
#ifdef CONFIG_HAVE_UNDERSCORE_SYMBOL_PREFIX
#define __VMLINUX_SYMBOL(x) _##x
#define __VMLINUX_SYMBOL_STR(x) "_" #x
#else
#define __VMLINUX_SYMBOL(x) x
#define __VMLINUX_SYMBOL_STR(x) #x
#endif

/* Indirect, so macros are expanded before pasting. */
#define VMLINUX_SYMBOL(x) __VMLINUX_SYMBOL(x)
#define VMLINUX_SYMBOL_STR(x) __VMLINUX_SYMBOL_STR(x)
```

就是根據 `CONFIG_HAVE_UNDERSCORE_SYMBOL_PREFIX` 設定與否，`VMLINUX_SYMBOL_STR(myfunction)` 可能會傳回 `myfunction` 或 `_myfunction`

第二個變數是第 11 行的 `__ksymtab_myfunction`，是一個 kernel_symbol 結構，用來表示一個核心符號，kernel_symbol 定義為

``` c include/linux/export.h
struct kernel_symbol
{
    unsigned long value;
    const char *name;
};
```

value 代表符號所在的位址，name 是符號的名稱

上面被定義的兩個變數 `__kstrtab_myfunction` 和` __ksymtab_myfunction` 會分別放在 `__ksymtab_strings`，`___ksymtab+myfunction` 這兩個 section 中，而這些 section 最後都會被連結器腳本統整到同一個地方，連結器腳本定義在 `include/asm-generic/vmlinux.lds.h`，這裡只列出一部分

``` c include/asm-generic/vmlinux.lds.h
/* Kernel symbol table: Normal symbols */           \
__ksymtab         : AT(ADDR(__ksymtab) - LOAD_OFFSET) {     \
    VMLINUX_SYMBOL(__start___ksymtab) = .;          \
    *(SORT(___ksymtab+*))                   \
    VMLINUX_SYMBOL(__stop___ksymtab) = .;           \
}

...

/* Kernel symbol table: strings */              \
    __ksymtab_strings : AT(ADDR(__ksymtab_strings) - LOAD_OFFSET) { \
    *(__ksymtab_strings)                    \
}
```

連結器腳本把所有 `___ksymtab+` 開頭的 section 放到 `__ksymtab` 裡；把所有 `__ksymtab_strings`
section 放到 `__ksymtab_strings` 裡，而 `__start___ksymtab`，`__stop___ksymtab` 則會在 `kernel/module.c` 被用到

``` c kernel/module.c
/* Provided by the linker */
extern const struct kernel_symbol __start___ksymtab[];
extern const struct kernel_symbol __stop___ksymtab[];
extern const struct kernel_symbol __start___ksymtab_gpl[];
extern const struct kernel_symbol __stop___ksymtab_gpl[];
extern const struct kernel_symbol __start___ksymtab_gpl_future[];
extern const struct kernel_symbol __stop___ksymtab_gpl_future[];
extern const unsigned long __start___kcrctab[];
extern const unsigned long __start___kcrctab_gpl[];
extern const unsigned long __start___kcrctab_gpl_future[];
```

有了這些資訊，當核心載入一個模組時，對於模組裡未解析的符號，便可以根據以上的變數，找到對應的符號，成功的載入

## Reference
[Kernel Symbols](http://www.linux.com/learn/linux-training/31161-the-kernel-newbie-corner-kernel-symbols-whats-available-to-your-module-what-isnt)
