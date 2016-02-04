---
title: npm教程
date: 2016-02-4 10:40:57
tags: npm
---

### 基本使用

* 安装与升级
	* 在安装 `node`的时候会自动安装`npm`
	* `sudo npm install npm -g`进行升级,使用`cnpm`的话，`sudo cpm install npm -g`进行升级


* 安装模块
  * 全局
    * 命令行等工具，使用全局安装
    * `npm install <package_name> -g`
  * 本地项目
    * 你项目中的各种依赖
    * `npm install <package_name>`


* 使用`package.json`
  * 在项目中管理`npm`模块，最好的方式是创建一个`package.json`的文件进行管理
  * 好处
    * 你依赖的各个模块在文件中都有记载
    * 可以让你指定模块的特定版本
    * 更好的协作性
  * `npm install <package_name> --save`安装模块，并写入`package.json`的`dependencies`字段
  * `npm install <package_name> --save-dev`安装模块，并写入`package.json`的`devDependencies`字段


* 升级模块
  * 本地模块
    * `npm outdated` 查看哪些需要升级
    * `npm update`进行升级
  * 全局模块
    * `npm outdated -g --depth=0`
    * `npm update -g` 升级全部模块


* 卸载模块
  * 本地
    * `npm uninstall lodash`删除模块
    * `npm uninstall --save lodash`，删除模块，并在`package.json`中移除
  * 全局
    * `npm uninstall -g jshint`

### 问题

* [提示`EACCES`error（两种解决方案）](https://docs.npmjs.com/getting-started/fixing-npm-permissions)
  1. 改变`npm`默认目录的权限
    * 找到`npm`的路径
      * ` npm config get prefix`
    * `sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}`
  2. 更改`npm`的默认目录
    * 创建一个新目录`mkdir ~/.npm-global`
    * `npm`配置到该目录 `npm config set prefix '~/.npm-global'`
    * 创建一个`~/.profile`文件，并写入 `export PATH=~/.npm-global/bin:$PATH`
    * 回到命令行，进行编译 `source ~/.profile`
