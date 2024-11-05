---
title: "windows 配置笔记"
categories: 笔记
tags: [windows]
---

> 因为最近频繁重装系统，而每次都要配置很久的环境，而大部分时间都在找教程了，因为具体内容记不住（也没必要记吧个人觉得）

## 个人使用习惯

### 交换 CapsLock 和左 Ctrl 键

进入注册表，依次找到 `HKEY_LOCAL_MACHINE --> System --> CurrentControlSet --> Control --> KeyBoard Layout`
右键` [KeyBoard Layout] `新建二进制值，并更名为 `[Scancode Map]`
然后键入值如下：

```
00 00 00 00 00 00 00 00
03 00 00 00 1D 00 3A 00
3A 00 1D 00 00 00 00 00
```

> 打开就知道怎么填了

重启生效[^1]

[^1]:[Windows 10 交换 Caps 和左 Ctrl 按键](https://lightjameslyy.github.io/windows-10-swap-caps-and-ctrl/) 

### Oh-My-Posh

~~主要是为了个性化~~使用了 oh-my-posh[^5]，缺点是启动较慢

[^5]:[oh-my-posh](https://ohmyposh.dev/)

### PowerShell Emacs mode

在`$PROFILE` 中加入

```
Set-PSReadLineOption -EditMode Emacs
```

### 字体

等宽字体 Sarasa Term SC Nerd Font[^2]
[^2]:[Sarasa Term SC Nerd](https://github.com/laishulu/Sarasa-Term-SC-Nerd)

## DevTool

### VSC 和 JB ide 主题

使用的是 moegi[^3]，亮色主题不那么刺眼。

[^3]:[Moegi.Design](https://github.com/moegi-design)

### Git

ssh 流量走代理比较麻烦，所以 github 改用 github-cli[^6] 了
[^6]:[GitHub CLI | Take GitHub to the command line](https://cli.github.com/)

## 以前备份的 linux 下的 config

偶尔连服务器可能要配置一下 tmux 和 vim[^4]

[^4]:[B1ink2's dotfile](https://github.com/b1ink2/dotfile)

# ENDING
> 你问我为什么不只用 Linux？要打游戏的嘛
