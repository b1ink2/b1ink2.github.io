---
title: "树莓派 3B 安装 Archlinux Arm"
categories: 笔记
tags: [archlinux, rasp]
---

## 准备
- SD 卡
- 一台安装好 linux 的电脑
- 一台树莓派 3B

## 安装

### 分区

首先吧 SD 卡插到电脑，将其格式化为一个 `256M boot` 分区和一个 `root` 分区。

使用该命令进行分区，`sdX` 换成对应的 SD 卡。

```bash
fdisk /dev/sdX
```
1. 输入 `o` 删除所有分区
2. 输入 `p` 列出所有分区，此时应该为空
3. 输入 `n` 创建一个分区，`p` 表示主分区，`1` 表示分区号，`Enter` 使用默认起始扇区，`+256M` 表示大小
4. 输入 `t` 设置分区类型，`c` 表示 W95 FAT32 (LBA)
5. 输入 `n` 创建一个分区，`p` 表示主分区，`2` 表示分区号，`Enter` 使用默认起始扇区，`Enter` 使用默认结束扇区(即所有剩余空间)
6. 输入 `p` 列出所有分区，此时应该有两个分区
7. 输入 `w` 写入分区表并退出

### 文件系统

把第一个分区格式化为 FAT 文件系统，并挂载到 boot 目录
```bash
mkfs.vfat /dev/sdX1
mkdir boot
mount /dev/sdX1 boot
```

把第二个分区格式化为 ext4 文件系统，并挂载到 root 目录

```bash
mkfs.ext4 /dev/sdX2
mkdir root
mount /dev/sdX2 root
```

> 注意，我不确定这是我自己的问题还是一个再正常不过的情况。我在使用 `fdisk` 分区完成后，执行后续写入系统的命令时，会遇到一个 SD 卡占用的错误，报错提示和权限有关。在网上找了很多也没有办法解决，最后是把 SD 卡分区这些弄好后，直接取消挂载(`fdisk` 上不显示)，但是还是按照 `/dev/sdX` 执行命令才写入成功（这个就很莫名其妙）。这也是写这篇博客的主要原因，毕竟网上优秀的教程一大把。

### 写入系统

下载系统镜像，并解压到 SD卡。

```bash
wget http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-armv7-latest.tar.gz
bsdtar -xpf ArchLinuxARM-rpi-armv7-latest.tar.gz -C root
sync
```

> 最后的 `sync` 是同步命令，为了确保所有数据写入 SD 卡。

镜像地址可以换成国内的镜像源:

|镜像源|地址|
|---|---|
|清华源|https://mirrors.tuna.tsinghua.edu.cn/archlinuxarm/os/ArchLinuxARM-rpi-armv7-latest.tar.gz|
|科大源|https://mirrors.ustc.edu.cn/archlinuxarm/os/ArchLinuxARM-rpi-armv7-latest.tar.gz|

> 树莓派 3B+ 往后的建议用 aarch64

写入 boot 分区，并取消挂载

```bash
mv root/boot/* boot

umount boot root
```

## 配置

插入SD 卡、电源，启动树莓派。建议插个网线 SSH 登录

|用户|账户|密码|
|--|--|--|
|root|root|root|
|user|alarm|alarm|

### 修改密码

修改 root 密码

```bash
passwd
```

添加用户
```bash
useradd -m {username}
passwd {password}
```

# ENDING

> 2025 新年快乐🎇