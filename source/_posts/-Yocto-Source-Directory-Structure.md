title: "[Yocto] Source Directory Structure"
date: 2015-01-11 13:29:05
categories: Yocto
tags:
- Yocto
---

簡單介紹 [Yocto Project](https://www.yoctoproject.org/) 的目錄結構

<!-- more -->

## Yocto Directory Structure

在 Yocto 的目錄裡，有以下的目錄跟檔案 (版本為 1.7)

* bitbake/
* build/
* documentation/
* meta/
* meta-yocto/
* meta-yocto-bsp/
* meta-selftest/
* meta-skeleton/
* scripts/
* oe-init-build-env
* oe-init-build-env-memres
* LICENSE, README, and README.hardware

---

### bitbake/

放 BitBake project 目前 release 版本的複製，BitBake 用來分析 Metadata，並且執行 Metadata 裡所定義的工作，當輸入 bitbake 指令的時候，`bitbake/bin/bitbake` 會被執行

### build/

一開始並沒有這個目錄，必須要執行 `source oe-init-build-env` 或 `source oe-init-build-env-memres` 之後才會自動建立，這個目錄放置設定檔還有所有的建置結果

### documentation/

顧名思義，就是放教學還有說明文件的地方

### meta/

放與 OpenEmbeded Core 有關的 metadata，有預設的指引檔 (recipes)，常用的類別檔 (classes)，模擬的目標機器設定值 (qemux86)

### meta-yocto/

包含與 Poky distribution 有關的設定

### meta-yocto-bsp/

存放與 BSP 有關的設定

### meta-selftest/

多加了指引檔與附加檔案，用來測試建立系統時的行為，通常在 `bblayers.conf` 都不會加上這一層，除非要做測試

### meta-skeleton/

當想要測試自己的 BSP 或 kernel，這裡提供預設的範本

### scripts/

放置一些建構會用到的腳本與指令

### oe-init-build-env

這是設定 OpenEmbedded build 環境的檔案，當執行 `source oe-init-build-env` 之後，路徑 `scripts/:bitbake/bin/` 會被加入到 PATH 裡，並且會建立 `build/` 目錄並移動到目錄裡，而且將 TOPDIR 變數指向 `build/`

### oe-init-build-env-memres

目前還不是很清楚，大致上看起來與 oe-init-build-env 相同，差別只在於 BitBake 會常駐在記憶體裡

### LICENSE, README, and README.hardware

與 license 有關的資料與 yocto 的介紹

