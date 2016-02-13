---
title: 如何判断页面是否在iframe中
date: 2016-01-21 22:12:57
tags: javascript
---

卧槽。。。我做前端这么久，一直没接触过`iframe`，最近在搞登录，总算是有机会接触下这玩意了。

然后开发和我说在登录中要判断我们自己的页面是否是在`iframe`中，当时我就 **懵逼** 了。当时的第一想法是，这搞不定吧。后面`google`了一下，发现还是可以搞定的。

就是判断`window`对象上的`top`属性是否等于自己。

```
if (window.top === window) {
  console.log('我不在iframe中');
} else {
  console.log('我在iframe中');
}
```

* 那`top`对象是什么鬼呢
  * top 属性返回最顶层的先辈窗口。
该属性返回对一个顶级窗口的只读引用。
  * 如果窗口本身就是一个顶级窗口，top 属性存放对窗口自身的引用。如果窗口是一个框架，那么 top 属性引用包含框架的顶层窗口。

说的通俗一点就是，让你在iframe中的时候，top就是引用你的页面的window对象；当你不在的时候，就是自己的window对象了

```
<!-- father.html -->
<html>
  <head>
  </head>
  <body>
    <iframe src="./chind.html"></iframe>
    <script>
      console.log(window === window.top); // 没有父窗口，就是top就是window
    </script>
  </body>
</html>

<!-- child.html -->
<html>
  <head>
  </head>
  <body>
    <script>
      console.log(window === window.top); // 父窗口是father.html,所以window.top是father.html的window
    </script>
  </body>
</html>
```
