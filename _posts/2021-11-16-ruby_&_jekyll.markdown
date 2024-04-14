---
title: 'Jekyll & Ruby'
categories: 笔记
tags: [jekyll, ruby]
---

## 前提

今年在大学里终于装了一台台式机，但是天煞的矿工把显卡炒的价格高的离谱，只能用一张亮机卡带我的新屏幕，**新屏幕敲代码真的很爽！**不过，也如你所见这个博客没更新的时间长的离谱，这也意味着我得重新配置这个本地预览博客的**Ruby**环境。不仅如此，长期不使用也意味着很有可能原先的配置已经过时，不再适用。

## 安装Ruby、gem、bundler

> wsl真的很方便，没有特殊说明都是在wsl ubuntu20.04LTS的环境下。

```shell
sudo apt install ruby ruby-dev gem ruby-bundler    # 安装ruby gem bundler
gem sources --add https://mirrors.tuna.tsinghua.edu.cn/rubygems/ --remove https://rubygems.org/    # 替换gem源为清华源 #
gem sources -l # 列出的网址应该只有Tsinghua的一个
bundle config mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems # 替换bundler源为清华源 #
```

完成了上面的工作可以让接下来的事情变得顺利一点，至少不用为了网络问题发愁。

## 克隆GitHub Page的代码，并启动jekyll

``` shell
git clone "你的GitHub Page项目地址"

cd ./"你的GitHub Page项目文件夹"
bundle exec jekyll serve
```

此时就能在浏览器`http://127.0.0.1:4000`预览效果了。~~默认是4000端口~~

注意：如果你是第一次使用GitHub Page，在github上找一个你认为顺眼的主题并按文档应用他们吧！但如果你像我一样是突然心血来潮了，那就继续看下去吧。

## 一些小问题

理论上按照[Jekyll的网站 (jekyllcn.com)](http://jekyllcn.com/)你就可以开始你的博客生活了，但我在第一步就遇到了问题：

``` shell
bundle install

An error occurred while installing eventmachine (1.2.7), and Bundler cannot continue.
An error occurred while installing http_parser.rb (0.8.0), and Bundler cannot continue.
```

无法下载`eventmachine`和`http_parser.rb`。我又尝试了`gem install jekyll ` 仍然有报错。在搜索的过程中，提到有可能是路径的问题，也有可能是版本的问题，我更倾向于后者。但是我看到一个解决办法：

```shell
gem install --user-install bundler jekyll
```

依然没有成功，但是在阅读报错信息的时候发现是在编译的时候找不到`make`命令。~~多么令人无语~~。因为第二次运行它提示我甚至没有`g++`。

```shell
sudo apt install make g++
```

接着就可以愉快的玩耍了。

**此时只需：**

```shell
bundle exec jekyll serve
```

就能愉快的码字了。但还没完，GitHub提示我有两个安全问题，`kramdown`和`addressable`版本过低所致。在GitHub上这个主题的源项的`gemfile`目里面找到Jekyll版本要求，并添加如下配置：

```ymal
jekyll, ">= 3.5", "< 5.0"

gem "kramdown", ">= 2.3.1"
gem "addressable", ">= 2.8.0"
```

保存文件，运行：

```shell
bundle

bundle exec jekyll serve
```

至此，问题相对顺利的解决，但又没有完全解决。因为还有一些地方需要更新，此时只是勉强能够运行。

# ENDING

> 感谢阅读，祝您生活愉快。
