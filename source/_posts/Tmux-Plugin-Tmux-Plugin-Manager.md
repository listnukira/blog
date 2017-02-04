title: '[Tmux][Plugin] Tmux Plugin Manager'
date: 2017-02-02 01:02:56
categories: Tmux
tags: Tmux
---
[Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)

<!-- more -->

### TPM Installation

#### 自動安裝
[Automatic tpm installation](https://github.com/tmux-plugins/tpm/blob/master/docs/automatic_tpm_installation.md)
在 .tmux.conf 裡新增以下這段
```
if "test ! -d ~/.tmux/plugins/tpm" \
   "run 'git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm && ~/.tmux/plugins/tpm/bin/install_plugins'"
```
這段要在 run '~/.tmux/plugins/tpm/tpm' 之前，加完後重新啟動 Tmux

#### 手動安裝
直接抓 TPM 到 ~/.tmux/plugins/tpm
```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### TPM Configuration
將建議的設定放到 .tmux.conf 裡
```
# List of plugins
# set -g @plugin 'github_username/plugin_name'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

### TPM Usage
安裝 plugin
   1. 在 .tmux.conf 裡加上 `set -g @plugin '<plugin>'`
   2. 按 prefix + I 安裝

更新 plugin
   1. 按 prefix + U 更新

移除 plugin
   1. 在 .tmux.conf 裡把要移除的 plugin 刪除或註解
   2. 按 prefix + alt + u，移除
