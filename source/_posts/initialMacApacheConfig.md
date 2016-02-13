---
title: mac初始化配置apache启动目录
date: 2016-02-13 10:40:57
tags: mac
---

#### 此文章的目的是把`apache`的默认启动目录改为当前的用户目录

默认情况下mac下apachectl配置的默认路径是

```
/Library/WebServer/Documents
```

我们可能需要在本地的服务器上访问我们的文件，通过这个地址我们很不方便的访问我们需要的文件，我们可以修改我们apachectl的根目录来快速的访问到我们需要访问的文件。

#### 第一步
---
我们需要找到apachectl的配置文件

```
cd /etc/apache2
```

```
vim httpd.conf
```

#### 第二步
---
在文件中搜索
`<Directory "/Library/WebServer/Documents">`
将`Options FollowSymLinks Multiviews `修改为`Options Indexes FollowSymLinks Multiviews`

因为系统级根目录默认没有开启目录列表，这个修改则开启了目录列表

在终端上输入

`cd && pwd`
查看你当前用户级的目录地址```/Users/username```

将
`<Directory "/Library/WebServer/Documents">`替换为`<Directory "/Users/username">`
`#DocumentRoot "/Library/WebServer/Documents"`替换为`#DocumentRoot "/Users/username"`

#### 第三步
---
这个时候我们去打开我们的localhost访问是，会提示没有权限，这个时候我们需要在配置文件下面添加```username.conf```添加我们的用户信息，将文件保存在```/etc/apache2/users/```下。这里需要使用```sudo```权限。

### 其他

更多信息可以参考[这篇文章](http://note.rpsh.net/posts/2013/11/27/osx-10-9-apache-server-php-mysql/)













