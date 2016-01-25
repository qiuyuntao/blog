---
title: git 版本回退 -- git log 和 git reflog 的区别
date: 2016-01-25 21:40:57
tags: git
---

### 背景

今天代码写着写着，就发现在IE8有问题，但是在改代码之前是没问题的。这个时候我就决定先`commit`我的代码，然后`reset`到我刚才`pull`的远程最新版本上去。

回退完之后，也看出是什么问题了，我就想回到我刚才`commit`的那个时候去，执行了`git log`命令，这个时候我傻眼了，麻痹的我的`commit`记录没了。当时无所个草泥马在眼前，当时就呆在那坐了回，骂了半天，什么鬼。

### 解决方案

然后我就去`google`了一下（总不能让我重新写我写了一上午的东西吧），我觉得我`commit`过了，肯定不会有问题的，代码一定还在。果不出其然，我发现了还有一个命令`git reflog`，执行了之后，找到了我刚才`commit`的`id`，直接`git reset --hard xxx`，找回了我之前的代码。

### 原理

  * [git log](http://git-scm.com/docs/git-log)
    * `git log`展示的是当前的`HEAD`以及它之前的各种信息。等于它只能找到之前的各种`commit`、`merge`等信息。
    * 所以在我`reset`之后，找不到我`commit`的记录，因为这次的`commit`是在此时`HEAD`之后进行的。
  * [git reflog](https://www.git-scm.com/docs/git-reflog)
    * `git reflog`记录了你的目录下任意时刻的`commits`。所以就算我`reset`了，依旧会有我的记录。

### 总结
所以说，只要你`commit`过，始终`reflog`绝壁是能找到你的`commit`记录的

"Keep calm and use `git reflog`"

[参考文档](http://stackoverflow.com/questions/17857723/whats-the-difference-between-git-reflog-and-log)
