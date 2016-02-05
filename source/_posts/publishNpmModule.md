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


* `npm`tags
  * 安装`npm`包的时候，可以使用`npm install qyt-test`来安装，或者使用`npm install qyt-test@1.0.0`、`npm install qyt-test@beta`来安装
  * @后面的标识符就是我们`npm publish`发布所打的`tag`。
  * 默认情况，发布版本的时候会打上你的`package.json`的version做为tag。
    * 例如你的`package.json`里的`"version": "1.0.3"`，你安装的时候就可以使用`npm install qyt-test@1.0.3`
  * 同时默认情况下，会在最后一次的`npm publish`中给你打上`latest`的tag
    * 例如你的最后一次发布`package.json`里的`"version": "1.0.3"`，你安装的时候就可以使用`npm install qyt-test@1.0.3`以及`npm install qyt-test@latest`
  * 你也可以增加其他的`tag`
    * `npm dist-tag add <pkg>@<version> [<tag>]`  例如 `npm dist-tag qyt-test@1.0.3 beta`
    * 你也可以直接在发布的时候`npm publish --tag beta`
    * 如果你想给已经发布过的模块打`tag`，也是使用`npm dist-tag qyt-test@1.0.0 beta`
  * 删除`tag`
    * `npm dist-tag rm <pkg> <tag>`
    * 例如`npm dist-tag rm qyt-test beta`
  * 查看模块`tag`
    * `npm dist-tag ls [<pkg>]`
    * 例如 `npm dist-tag ls qyt-test`


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
