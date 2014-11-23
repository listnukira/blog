title: "[Linux Kernel] Notification chain"
date: 2014-10-13 23:33:19
categories: Linux Kernel
tags: Linux Kernel
---
Linux Kernel 用 Notification chain 來傳遞事件的發生或是狀態的改變，Notification chain 以 publish-subscribe 的機制運作，與 polling 或 request-reply 相比，Notification chain 更有效率，需要訊息的元件自己註冊，當事件發生或狀態改變時，便通知所有註冊的元件

## Notification chain

與 Notification chain 相關的定義與函式幾乎都在 `include/linux/notifier.h` 和 `kernel/notifier.c` 這兩個檔案裡

### 類型

目前 Linux Kernel 有四種不同類型的 Notification chain

* Atomic notifier chains
給重要事件使用，callback 函式不能被 block 住
* Blocking notifier chains
當在執行的時候允許被 block 住
* Raw notifier chains
對 callback 函式沒有限制，用來處理比較低階的事件
* SRCU notifier chains
與 blocking notifier chain 很像，差別在於保護的方式，SRCU notifier chain 使用 SRCU 取代 rw-semaphores

其它更詳細的說明可以直接參考 `include/linux/notifier.h`

### 定義

不管是哪一種類型的 Notification chain，都是由 notifier_block 結構所組成的串列，notifier_block 定義在 `include/linux/notifier.h`

``` c include/linux/notifier.h
typedef int (*notifier_fn_t)(struct notifier_block *nb,
            unsigned long action, void *data);

struct notifier_block {
    notifier_fn_t notifier_call;
    struct notifier_block __rcu *next;
    int priority;
};
```

notifier_block 中的 notifier_call 代表 callback 函式

### 註冊

當一個核心元件對特定通知鏈的事件感興趣時，可以用通用函式 notifier_chain_register 向它註冊，但是通常都會透過包裹函式來註冊

以跟網路程式碼相關的通知鏈 netdev_chain (net/core/dev.c) 為例，它被初始化為 Raw notifier chains 的類型
`static RAW_NOTIFIER_HEAD(netdev_chain);`

初始化之後，其他元件便可以利用包裹函式 register_netdevice_notifier 註冊，而 register_netdevice_notifier 會再呼叫 raw_notifier_chain_register 註冊

### 事件

通知訊息產生自 notifier_call_chain (kernel/notifier.c)，會向所有註冊的元件發送訊息
例如當一個裝置要註冊為網路裝置時，會呼叫 register_netdevice (net/core/dev.c)，裡面會呼叫到包裹函式 call_netdevice_notifiers，並把 NETDEV_REGISTER 這個事件往通知鏈傳送，所有已註冊的裝置都會收到

### 範例

以 ARP 子系統為例，當核心初始化 ARP 子系統時，會執行初始化函式 arp_init (net/ipv4/arp.c)，函式裡面會呼叫 register_netdevice_notifier，向 netdev_chain 註冊名稱為 arp_netdev_notifier 的 notifier_block 結構，並且把成員函式 notifier_call 也就是 callback function 設為 arp_netdev_event

``` c net/ipv4/arp.c
void __init arp_init(void)
{
    ...

    register_netdevice_notifier(&arp_netdev_notifier);
}

...

static struct notifier_block arp_netdev_notifier = {
    .notifier_call = arp_netdev_event,
};
```

接下來再看看 arp_netdev_event 這個函式

``` c net/ipv4/arp.c
static int arp_netdev_event(struct notifier_block *this, unsigned long event,
                void *ptr)
{
    struct net_device *dev = netdev_notifier_info_to_dev(ptr);
    struct netdev_notifier_change_info *change_info;

    switch (event) {
    case NETDEV_CHANGEADDR:
        neigh_changeaddr(&arp_tbl, dev);
        rt_cache_flush(dev_net(dev));
        break;
    case NETDEV_CHANGE:
        change_info = ptr;
        if (change_info->flags_changed & IFF_NOARP)
            neigh_changeaddr(&arp_tbl, dev);
        break;
    default:
        break;
    }

    return NOTIFY_DONE;
}
```

從這個函式可以看到 ARP 子系統只會處理 NETDEV_CHANGEADDR 和 NETDEV_CHANGE 這兩個事件，其它的事件會忽略

在 `net/core/dev.c` 裡有個函式叫 `dev_set_mac_address`，這個函式會呼叫call_netdevice_notifiers，把 NETDEV_CHANGEADDR 這個事件往通知鏈 (netdev_chain) 傳送，每個註冊的裝置都會對這個事件做處理或者忽略它

## Reference site

[The Crux of Linux Notifier Chains](http://www.opensourceforu.com/2009/01/the-crux-of-linux-notifier-chains/)
