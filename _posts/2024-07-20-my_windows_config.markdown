---
title: "windows 配置笔记"
categories: 笔记
tags: [windows]
---

> 因为最近频繁重装系统，而每次都要配置很久的环境，而大部分时间都在找教程了，因为具体内容记不住（也没必要记吧个人觉得）

## 个人使用习惯

### 交换CapsLock和左Ctrl键

进入注册表，依次找到 HKEY_LOCAL_MACHINE --> System --> CurrentControlSet --> Control --> KeyBoard Layout
右键 [KeyBoard Layout] 新建二进制值，并更名为 [Scancode Map]
然后键入值如下：

```
00 00 00 00 00 00 00 00
03 00 00 00 1D 00 3A 00
3A 00 1D 00 00 00 00 00
```

> 打开就知道怎么填了

重启生效[^1]

[^1]: https://lightjameslyy.github.io/windows-10-swap-caps-and-ctrl/ 

### PowerShell Emacs mode

```
Set-PSReadLineOption -EditMode Emacs
```

## DevTool

### VSC 和 JB ide 主题

moegi[^2]

[^2]: https://github.com/moegi-design

### Git

ssh 流量走代理比较麻烦，所以 github 改用 github-cli 了

## 以前备份的 linux 下的 config

https://github.com/b1ink2/dotfile
https://gitee.com/Ray_T/config

> 偶尔连服务器可能要配置一下 tmux 和 vim 会用到

#### TODO: 不定期更新