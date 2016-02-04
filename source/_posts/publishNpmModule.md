---
title: 发布一个npm模块
date: 2016-02-4 15:40:57
tags: npm
---

发布模块
---
* 创建新目录
  * `npm init`
  * 自动生成`package.json`
  * `name`和`version`是必须要的
  * `name`为`qyt-test`



* 创建`index.js`
  ```
    export.printMsg = function() {
      console.log('this module name is qyt-test');
    }
  ```

* `package.json`里有一个`main`字段，默认引入的就是这个字段的文件
  * `"main": "index.js"`
  ```
    var aMoudle = require('qyt-test');
    /**
    * aMoudle 就是 index.js里输出的内容
    **/
  ```


* 注册`npm`账号（两个方法）
  1. [注册地址](https://www.npmjs.com/)
  2. `npm adduser`


* `npm`登录
  * `npm login`


* `npm`模块发布
  * `npm publish`


使用你发布的模块
--

* 创建路径

  ```
    mkdir test
    cd test
    npm init
    npm install qyt-test
    touch index.js
  ```


* 创建文件
  ```
    touch index.js

    /**
    * in index.js
    **/
    var a = require('qyt-test');
  ```


* 执行
  `node index.js`会输出`this module name is qyt-test`
