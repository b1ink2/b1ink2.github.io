---
title: "磨刀不误砍柴工，优化wsl"
categories: 笔记
tags: [wsl]
---

## 准备

> WSL
> Fluent Terminal

WSL[^1] 在 win10 自带的应用商店里搜索 Linux 选择自己喜欢的 Linux 发行版点击安装（本文使用 Ubuntu）。

[^1]:[Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/)

安装完成后别忘了打开`控制面板->程序->启用或关闭 Windows 功能->适用于 Linux 的 Windows 的子系统`打上勾，然后就可以运行 WSL 了。~~如果不行，那就重启。~~

第一次运行 WSl 会提示输入用户名和设置密码。

接下来安装 Fluent Termianl[^2] *你也可以使用其他终端程序*。


下载完成后右键 `install.ps1-->在 powershell 中运行`，根据提示安装即可。

安装完成后可以在`settings->profiles把wsl设置成默认项`也可以键入`ctrl+alt+3`打开一个 WSL 的标签页。

[^2]:[Fluent Terminal](https://github.com/felixse/FluentTerminal/archive/master.zip) 

## 美化

运行以下命令安装 zsh

```terminal
sudo apt-get install zsh
```

再运行

```terminal
chsh -s /bin/zsh
```

将默认 bash 设置成 zsh，重启 terminal 看到的就是 zsh 的样子了。但是默认主题不是很好看，下面就要安装 oh-my-zsh 给它找个漂亮的外套。

```terminal
wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
```

### 主题

找个好看的主题[^3]记下他的名字，接着在`~/.zshrc`里找到`ZSH_THEME`把后面的内容替换掉就好。

[^3]:[oh-my-zsh themes](https://github.com/ohmyzsh/ohmyzsh/wiki/themes)

### 字体

如果看中了 agnoster 等主题需要一些特殊字符才行，比如 fira code 等 nerd font [^4]。下载完成后在双击在左上角点击安装。安装完后在fluent terminal->settings -> terminal 字体里找到刚安装的字体，主题就能正常显示了。

[^4]:[Nerd Fonts Download](https://raw.githubusercontent.com/tonsky/FiraCode/master/distr/ttf/FiraCode-Retina.ttf)

### 插件

> syntax-highlighting & zsh-autosuggestions>
> 语法高亮与语法补全

在`~/.zshrc`添加

```terminal
plugins = (zsh-autosuggestions zsh-syntax-highlighting)
```

然后重启 terminla 就能看到最终的样子了。

# ENDING

### 2022.2.28
Windows 下改用 `windows terminal` 了。微软自家的，用起来很舒服。
Linux 用的 'Kitty' 功能很强大。