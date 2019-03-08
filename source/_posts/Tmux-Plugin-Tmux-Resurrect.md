title: '[Tmux][Plugin] Tmux Resurrect'
date: 2017-02-05 00:41:47
categories: Tmux
tags: Tmux
---
[Tmux Resurrect](https://github.com/tmux-plugins/tmux-resurrect) 用來儲存與回復開啟的 window/pane 與 layout

<!-- more -->

### Installation
用 TPM 安裝，在 .tmux.conf 新增

```
set -g @plugin 'tmux-plugins/tmux-resurrect'
```

然後按 prefix + I 安裝

### Usage

**Save**
`prefix + Ctrl-s`
**Restore**
`prefix + Ctrl-r`
