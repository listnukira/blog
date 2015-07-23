title: '[Linux Kernel] Coding style'
date: 2015-07-23 22:47:46
categories: Linux Kernel
tags: Linux Kernel
---

整理與記錄 Linux Kernel 的 coding style

<!-- more -->

## 每行程式碼的長度 Breaking long lines and strings

程式碼每行長度不能超過 80 個字元，超過就必須被合裡的換行，函式如果參數太長，也必須換行

但是像 `printk` 所印出來的訊息則不能被換行

## 縮排 Indentation

使用 Tab，Tab 代表八個字元，八個字元的 Tab 可以更明確的區分程式碼區塊，有些人覺得八個字元太多了，縮排個幾次就會超過每行 80 字元的限制，照核心開發者社群的說法，程式碼如果縮排太深，就必須考慮重構程式碼，讓程式碼看起來更簡單易懂

## 大括號 Braces

大括號要放在哪裡是根據 K&R 的 C 語言風格，除了函式以外，對於像 `if, switch, for, while, do` 這些關鍵字，左大括號要放在第一行陳述句的最後，右大括號自成一行與第一行陳述句對齊

<pre>
if (x is true) {
        we do y
}

switch (action) {
case KOBJ_ADD:
        return "add";
case KOBJ_REMOVE:
        return "remote";
default:
        return NULL;
}
</pre>

對於函式來說，左右括號都應該自成一行

<pre>
/* Execption for function */
int function (int x)
{
        body of function
}
</pre>

如果像是 `if else, do while` 這種的陳述句，右大括號就不應該自成一列，而應該跟對應的陳述句擺在一起

<pre>
do {
        body of do-loop
} while (condition);

if (x == y) {
        ...
} else if (x > y) {
        ...
} else {
        ...
}
</pre>

有些不一定要放括號的陳述句，像是 `if, for`，可以不用放括號

<pre>
if (condition)
        action();

if (condition)
        action1();
else
        action2();
</pre>

但是像 `if else` 這種陳述句，只有其中一個不用放括號，而另一個要，則全部都要放括號

<pre>
if (condition) {
        do_this();
        do_that();
} else {
        do_else();
}
</pre>

## 空格 Spaces

在大多數的關鍵字後面都會加上空格，除了 `sizeof, typeof, alignof, __attribute__` 這些關鍵字

<pre>
if (condition)
while (condition)
for (i = 0; i < NR_CPUS; i++)
switch (condition)

s = sizeof(struct file);
typeof(*p)
__attribute__((packed))

</pre>

在圓括號裡面，引數前後不加空白，以下是錯誤示範

<pre>
/* bad */
s = sizeof( struct file );
</pre>

當宣告一個指標或一個回傳指標的函式，解參照運算子要放在變數名稱或函式名稱的旁邊

<pre>
char *linux_banner;
unsigned long long memparse(char *ptr, char **retptr);
char *match_strdup(substring_t *s);
</pre>

大部分的二元或三元運算子要在兩邊加上空格

`=  +  -  <  >  *  /  %  |  &  ^  <=  >=  ==  !=  ?  :`

一元運算子不加空格

` &  *  +  -  ~  ! -- ++`

## 命名 Naming

變數名稱或函數名稱不應該混合大小寫，也不應該使用[匈牙利命名法](https://en.wikipedia.org/wiki/Hungarian_notation)

全域變數或函式應該要取具描述性的名稱，如果有一個函式是用來計算有多少正在活動的使用者，那這個函式應該命名為 `count_active_users()`，而不是 `cntusr()`，對於區域變數則應該盡量簡短，對於一個迭代用的迴圈變數，應該取為 `idx` 或 `i`，而不是 `loop_counter` 或 `loopCounter`

## 型態別名 Typedef

核心開發者社群反對 typedef 的使用，像是 `vps_t` 這種東西，主要的想法是當在程式碼裡看到 `vps_t a` 時，並不能馬上確定 `vps_t` 真正代表的是什麼，他有可能被定義成 `typedef struct vps vps_t` 或 `typedef struct vps *vps_t`，而像 `struct virtual_container *a;` 就能很清楚的知道 `a` 代表什麼

## 函式 Function

函式的長度不應該超過一或兩個螢幕，區域變數不應該超過十個，函式與函式間須空一行，如果函式有用 `EXPORT*` 系列的巨集匯出，必須要緊跟在函式的右大括號下面

<pre>
int system_is_up(void)
{
        return system_state == SYSTEM_RUNNING;
}
EXPORT_SYMBOL(system_is_up);
</pre>

在宣告函式的原形時，儘管參數名稱不一定需要，也應該包含參數名稱，這樣可以提供更多資訊給閱讀的人

## 集中函式的返回區 Centralized exiting of functions

核心原始碼會合理的使用 `goto` 關鍵字來處理錯誤發生的情況

## 註解 Commenting

為程式碼寫註解是一件好事，但是不應該過分的註解。註解的內容應該是解釋程式碼在做什麼，而不是怎麼做，怎麼做應該由程式碼本身來表達，並且盡量避免在函式裡面寫註解，如果一個函式複雜到要寫很多註解在裡面，那麼就應該要考慮重構這個函式

核心原始碼傾向於使用 C89 風格的註解 ` /* ... */ `，所以不要使用 C99 風格的註解 ` // ... `，對於可能有很多行的註解則應該用下面的方式來寫

<pre>
/*
 * This is the preferred style for multi-line
 * comments in the Linux kernel source code.
 * Please use it consistently.
 */
</pre>

而在 `/net` 與 `drivers/net/` 下，多行註解沒有開頭的空行

<pre>
/* The preferred comment style for files in net/ and drivers/net
 * looks like this.
 */
</pre>

## 條件編譯 Conditional Compilation

盡量把 `#if, #ifdef` 放在 .h 檔裡而不要放在 .c 檔裡，放在 .c 檔裡會讓程式碼難以閱讀

## 其它

* 同一行程式碼不要有兩個 assign 陳述句

<pre>
/* bad */
a = 0; b = 3;
</pre>

* 同一行程式碼不要有兩個陳述句

<pre>
if (condition) do_this;
        do_something;
</pre>

* 在每一行的後面不要有空白

* switch 陳述句的 case 必須跟 switch 對齊，也就是在同一個縮排，如果想要從一個 case 穿越 (fall through) 到另一個 case 時，可以考慮加上註解

<pre>
switch (suffix) {
case 'G':
case 'g':
		mem = 30;
		break;
case 'M':
case 'm':
		mem = 20;
		break;
case 'M':
case 'm':
		mem = 10;
		/* fall through */
default:
		break;
}
</pre>

* `scripts/checkpatch.pl -f filename` 可以用來檢查檔案的 Coding style
