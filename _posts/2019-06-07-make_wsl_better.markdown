---
title: "磨刀不误砍柴工，优化wsl"
categories: 笔记
tags: [wsl]
---

# 一、准备

> wsl<br>
> fluent terminal

wsl在win10自带的应用商店里搜索Linux选择自己喜欢的Linux发行版点击安装（本文使用ubuntu）。

安装完成后别忘了打开控制面板->程序->启用或关闭Windows功能->适用于Linux的Windows的子系统打上勾，然后就可以运行wsl了。~~如果不行，那就重启。~~

第一次运行wsl会提示输入用户名和设置密码。

接下来安装[fluent terminal](https://github.com/felixse/FluentTerminal/archive/master.zip) *你也可以使用其他terminal*。

下载完右键install.ps1->在powershell中运行，根据提示安装即可。

安装完成后可以在settings->profiles把wsl设置成默认项也可以`ctrl+alt+3`打开一个wsl的标签页。

# <center>二、美化</center>

运行以下命令安装zsh

```
sudo apt-get install zsh
```

再运行

```
chsh -s /bin/zsh
```

将默认bash设置成zsh，重启terminal看到的就是zsh的样子了。但是默认主题不是很好看，下面就要安装oh-my-zsh给它找个漂亮的外套

```
wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
```

### 主题

找个好看的[主题](https://birdteam.net/131798)记下他的名字，接着在`~/.zshrc`里找到`ZSH_THEME`把后面的内容替换掉就好。

### 字体

如果看中了agnoster等主题需要一些特殊字符才行
需要下载字体[fira code](https://raw.githubusercontent.com/tonsky/FiraCode/master/distr/ttf/FiraCode-Retina.ttf)下载完成后在双击在左上角点击安装。安装完后在fluent terminal->settings -> terminal 字体里找到刚安装的字体，主题就能正常显示了

### 插件

> syntax-highlighting & zsh-autosuggestions<br>
> 语法高亮与语法补全

在`~/.zshrc`添加

```
plugins = (zsh-autosuggestions zsh-syntax-highlighting)
```

然后重启terminla就能看到最终的样子了

### 2022.2.28
windows 下的终端在用 'windows terminal' 微软自家的，用起来很舒服。
Linux 用的 'Kitty' 功能很强大