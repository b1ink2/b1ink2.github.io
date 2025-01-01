---
title: "从零开始使用 Github Pages 的搭建个人博客"
categories: 笔记
tags: [blog]
---

> 有一个自己的博客，而且能自己随心所欲的定制是一件很酷的事

### 准备

*   [GitHub](https://github.com/)账号

*   一个域名（可选）

*   [Cloudflare](https://dash.cloudflare.com/)账号（可选）

### Github Page

Github Page 是一个 GitHub 官方的项目，它使用 [jekyll](https://jekyllcn.com/) 对一个仓库提供静态网页的服务，理论上能做到任何网页能做的事情。
假设你的 GitHub 账户名叫做 "abc"，那么你只需要新建一个项目叫做 "abc.github.io"，此时你就创建了一个 Github Page 的项目。
接着你就可以在浏览器访问域名 "abc.github.io" 查看你的博客内容了。

#### 目录结构

```txt
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```

首先，`_config.yml` 里面是一些配置内容，不同主题里面的东西也不尽相同，请根据主题作者的介绍和自己的需要更改。
`_drafts` 和 `_posts` 里都是 Markdown 文件，不同在 `_drafts` 的内容不会在网站中显示，且非必须。`_posts` 是真正发布到网页上的内容。
`_includes` 和 `_layouts` 是网页的样式，前者是一个完整网页的格个部分，后者将若干个部分整合成完整的网页。如果需要外部引用 JS 脚本等就在 `_includes` 里的 `header.html` 中引用即可。
更具体的内容可以看 Jekyll 的官网[^1]。

[^1]:[Jekyll Home Page](https://jekyllcn.com/)

#### 主题

*   在 Github Page 设置页面可以从一些基础的主题中挑选一个。

*   在 Jekyll Themes[^2] 众多主题里选择一个并按说明执行操作即可。

*   在 GitHub 中寻找主题甚至别人的 Github Page 项目，Fork 一个，并改一下项目名称为 "abc.github.io"。

[^2]:[Jekyll Themes](https://jekyllthemes.org/) 

## 域名

域名并非必须，但是有一个域名也可以干一些有意思的事，比如更个性的邮箱、跳转到自己的一些社交账号等。
如果有域名了，那么我强烈建议使用 CDN 加速，因为在国内裸连 GitHub 的速度实在是不理想。

### DNS 配置
*如果不需要更换解析服务，可以略过本节*
如果你要用到如 CDN 加速等功能，而域名服务商无法提供时，我们就需要用其它服务商提供的 DNS 解析服务。
一个典型的例子：我在国内域名商购买了域名，如："blink.icu"。但是域名商的 CDN 服务需要付费，所以我想要使用可以免费提供 CDN 加速的 Cloudflare 来管理自己的域名。一般情况，Cloudflare 等服务商会提供一个 DNS 解析的服务器地址，然后在原域名商的平台那里替换掉就好。但是一般这种操作不是即时生效，需要耐心等一段时间，一般半小时左右，最多不超过 24 小时。
完成以上步骤后，域名解析的事情就由 Cloudflare 等第三方来解析，需要什么添加新的记录，如："blog.blink.icu"。 就在 Cloudflare 这些平台添加，而不是域名服务商的平台。

#### 域名解析

那么如何实现域名和网站的绑定呢？
最简单的方法是在域名解析里添加一个 CNAME 记录，如："blog.blink.icu" 直接指向自己的 "abc.github.io"。但是这种绑定是单向的，即实现了网页的跳转，但浏览器的域名还是 "abc.github.io"。如果要想实现双向的绑定，那么首先 github 服务器要知道有这样一个域名 "blog.blink.icu" 指向到 "abc.github.io"。然后在访问 "blog.blink.icu" 时，直接通知 github 服务器，返回 "abc.github.io" 的内容。

所以首先需要 A 记录，即 github 服务器的 IPv4 地址，一共 4 个，将他们添加到域名下面

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

然后需要一个 CNAME 将一个域名绑定到 "abc.github.io" 。比如我的这个域名就是 "blog.b1ink.icu" 那么我的 CNAME 记录值就是 "blog" 。如果是 "www" 就是我们最常见的域名了。

没有完，我们还需要在 GitHub 的仓库 Github Page 设置里的 CNAME 填写我们的域名。
截图可见下方 "”Cloudflare 配置" 小节。

## CDN 加速

在刚才经常提到 CDN 加速，其实很容易理解，它在世界各地布置有大量服务器，它将我们所访问的资源缓存在这些服务器中，我们访问时就不用从源服务器获取数据，而是从这些缓存好数据的服务器直接获取，因为地理位置、服务器数量等优势，所以可以有效提高静态网页的速度。

具体操作同下方 Cloudflare 配置过程大同小异，仅供参考

### Cloudflare 配置

Cloudflare 有比较良心的免费服务，很适合用在这种情况。注册完账号，添加网站(根域名)它会自动检测 DNS 解析服务。当配置的 DNS 解析服务生效后，我们就可以使用 CDN 加速了。一般情况会默认开启的。但是，我们需要先关闭一下，因为新版本的 Github Page 不能在这种情况下打开 HTTPS 我们将解析的代理情况关闭，变为 "仅 DNS 解析"。
然后在 Github Page 仓库的配置里打开 Enforce HTTPS。 同样的，生效需要一段时间。
接着，再回到 Cloudflare 打开代理即可。

> 这里打开强制 HTTPS 的方法可能不对，因为之前是没问题的，后来提示报错。我就用这种方法让它目前又正常工作了。

![Cloudflare 截图](https://img2.imgtp.com/2024/04/14/JA9w4UO7.png)

## 评论系统

我用的是 Valine[^3] 配置起来很方便，文档写的也很详细。

[^3]:[Valine:文章阅读量统计](https://valine.js.org/visitor.html) 

### 记一个问题
如果 markdown 文件的日期在未来某个时间，它会定时发布，但是这应该是 UTC 标准时间，所以大陆凌晨写好发出去可能不会立刻部署，可以把日期改成前一天的

# ENDING

> “新年快乐🧧”
