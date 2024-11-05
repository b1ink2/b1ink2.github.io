---
title: "Archlinux 折腾笔记"
categories: 笔记
tags: [archlinux]
---

# 引言

Archlinux 是个很需要折腾的 Linux 发行版，这里会记录一些折腾它遇到的一些问题。

不定期更新

# 软件

### Android Studio

Android 在大陆有服务器，可以通过改hosts文件访问

### easyconnect

aur 里有包，但是md5校验有问题，解决方法：手动下载到本地，执行 `makepkg -g >> PKGBUILD` 会自动覆盖原来的打包文件。执行
`sudo pacman -U easyconnect-XXX` 就能安装了

> 2022.5.22 再安装已经没有问题了

### Visual Studio Code

aur 源里有好几个， `visual-studio-code-bin` 这个是巨硬的，还有一个 `code` 是源代码编译的，有些扩展不能在商店里直接安装

### 中文输入法

以前一直用的是 fcitx 配合搜狗拼音食用。因为搜狗用的还是 fcitx-qt4，所以会有一些奇奇怪怪的问题，而且目前在用的 Gnome 桌面环境默认用的是 Ibus，所以这次就采用了 Ibus + rime 的组合，配置很简单

```shell
yay -S ibus ibus-rime
```

在 gnome 的设置里添加中文，并在 ibus-preferences 的 input method 里添加 rime 即可。

由于在 win 下习惯使用 `C-Space` 切换输入法，在 Gnome 里切换输入法直接在 Gnome 的快捷键设置里进行更改，Ibus-preferences 里的更改无效。



# 配置

### kitty

kitty 真的是我用过最舒服的终端，用显卡渲染，性能足够，支持图片，基本开箱即用，自己调整一下字体就行。

```shell
kitty +ktiiten themes
```

可以直接选择内置的主题，很丰富

### zsh

选择了 zim 管理 zsh 插件，p10k 也是真的好用。

### SSH 代理

首先安装 ncat

```shell
yay -S nmap
```

然后编辑`.ssh/config`，添加

```shell
Host github.com
    ProxyCommand ncat --proxy 地址:端口 --proxy-type socks5 %h %p
```

### i3+gnome

修改触摸板双击和自然滚动
编辑 `/etc/X11/xorg.conf.d/90-touchpad.conf`
添加

```shell
Section "InputClass"
	Identifier "touchpad"
	MathIsTouchpad "on"
	Driver "libinput" "on"
	Option "Tapping" "on"
	Option "NaturalScrolling" "on"
	Option "TappingButtonMap" "lrm"
```

交换 `caps lock` 和 `ctrl`
> 强烈建议这样做，尤其 shell 和 Emacs 重度用户

```sh
setxkbmap -option ctrl:swapcaps
```

### 声音

本来 gnome 有声音的，用了 Gnome i3 后 i3 和 gnome 都没声了。

> 会导致音频无声，以及无法播放音频和视频的情况。

本来以为是驱动问题，但是各种安装，重装都没用，还安装了 pulseaudio, 问题就在这，最后使用 pipewire 和 pipewire-pules 代替pulseaudio.


# ENDING

> BTW, I'm arch user.