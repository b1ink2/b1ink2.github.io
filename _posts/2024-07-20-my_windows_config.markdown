---
title: "windows 配置笔记"
categories: 笔记
tags: [windows]
---

> 因为最近频繁重装系统，而每次都要配置很久的环境，而大部分时间都在找教程了，因为具体内容记不住（也没必要记吧个人觉得）

## 个人使用习惯

### 交换 CapsLock 和左 Ctrl 键

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

### Oh-My-Posh

[oh-my-posh](https://ohmyposh.dev/)

### PowerShell Emacs mode

在`$PROFILE` 中加入

```
Set-PSReadLineOption -EditMode Emacs
```

### 字体

[Sarasa Term SC Nerd](https://github.com/laishulu/Sarasa-Term-SC-Nerd)

## DevTool

### VSC 和 JB ide 主题

moegi[^3]

[^3]: https://github.com/moegi-design

### Git

ssh 流量走代理比较麻烦，所以 github 改用 github-cli 了

## 以前备份的 linux 下的 config

[gitee](https://gitee.com/Ray_T/config)

[github](https://github.com/b1ink2/dotfile)

> 偶尔连服务器可能要配置一下 tmux 和 vim 会用到

#### TODO: 不定期更新