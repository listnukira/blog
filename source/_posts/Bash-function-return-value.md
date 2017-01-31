title: Bash 函式回傳值
date: 2016-11-29 00:39:22
categories: Linux
tags: Bash
toc: false
---

Bash 的函式與大部分程式語言不同，它的函式只能回傳整數數值，代表這個函式成功或失敗 (0 代表成功，非 0 代表失敗)，回傳的值可以由 `$?` 取得，如果函式裡面沒有明確的 return 述句，則 `$?` 的值會是最後一個指令的執行結果，有三種方法可以傳回整數以外的值

<!-- more -->

1.全域變數

```bash
func()
{
    result='return value'
}

func
echo $result
```

2.指令替換，函式裡使用 echo

```bash
func()
{
    local result='return value'
    echo "$result"
}

result=$(func)
echo $result
```

3.把結果放在傳進去的參數

```bash
func()
{
    eval $1="'return value'"
}

func1()
{
    local __resultvar=$1
    local __result='return value'
    eval $__resultvar="'$__result'"
}

func result
echo $result
```

---

Reference:
http://www.linuxjournal.com/content/return-values-bash-functions

