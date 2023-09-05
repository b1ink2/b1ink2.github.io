---
title: Emacs Org Mode
categories: 笔记
tags: [emacs]
---

# Emacs Org Mode

> Emacs is the extensible, customizable, self-documenting real-time display editor.

Org-mode是emacs的一个强大的工具，它可以用来写博客，记笔记，做计划，~~记日记~~。在这只简要的介绍几个功能

### 快捷键

| 快捷键       | 功能                |
|:------------:|:-------------------:|
| Tab          | 一级展开 全部展开 折叠 三种状态循环 |
| C-c C-n/p    | 下/上一个标题             |
| C-c C-f/b    | 下/上一个标题(同级标题下) |
| M-RET        | 插入同级标题              |
| M-S-RET      | 插入同级TODO              |
| M-LEFT/RIGHT | 表题升级/降级             |

### 特殊字体

按着Markdown和LaTeX琢磨吧<br>
注:<br>

{% highlight html %}
+删除线+
_下划线_
=等宽=
{% endhighlight %}

### 表格

按“`表头|表头`”的格式键入“`C-c RET`”就能快捷建立表格，tab键在表格内跳转(会自动新增下一行)

### 代码块

{% highlight html %}
#+BEGIN_SRC language
  balabalabala
#+END_SRC

{% endhighlight %}

键入“M-x org-edit-src-code”，就可以在相应的模式下编辑这段代码，简单说就是新建立个窗口，有相应的补全等功能

#### 就先写这么多吧

## 叛变！
vscode真的很好用，配置起来也挺方便的，但是有一点，插件多了可能会出现一些奇怪的bug或冲突，而且快捷键位有点难受。（2022.2.28）