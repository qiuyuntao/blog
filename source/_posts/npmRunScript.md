---
title: npm start 和 npm run start
date: 2016-01-27 10:40:57
tags: node
---

### 背景

在项目的目录中，我们会在 `package.json` 里配置 `scripts`项

```
  {
    "name": "hexo-site",
    "version": "0.0.0",
    "private": true,
    "hexo": {
      "version": "3.1.1"
    },
    "dependencies": {
      "hexo": "^3.1.1",
      "hexo-generator-archive": "^0.1.3",
      "hexo-generator-category": "^0.1.3",
      "hexo-generator-index": "^0.2.0",
      "hexo-generator-tag": "^0.1.2",
      "hexo-renderer-ejs": "^0.1.0",
      "hexo-renderer-stylus": "^0.3.0",
      "hexo-renderer-marked": "^0.2.6",
      "hexo-server": "^0.1.2"
    },
    "scripts": {
      "start": "hexo server",
      "publish": "hexo generate"
    }
  }

```
在这里你可以直接使用 `shell` command `npm start`去起hexo server，在端口中查看你的修改。
但是你会发现，我操`npm publish`是没用的。

### 为什么会这样

遇到这种问题，肯定要去看看文档啊。[npm-run-script](https://docs.npmjs.com/cli/run-script)。
文档里是这么说的 `If no "command" is provided, it will list the available scripts. run[-script] is used by the test, start, restart, and stop commands, but can be called directly, as well`,也就是说 `test, start, restart, and stop`这几个命令是不用加`run`，其他几个都是要加`run`。

所以，想要`publish`的话，就需要`npm run publish`就可以了。

### 参考文档

* [npm-run-script](https://docs.npmjs.com/cli/run-script)。
* [npm-scripts](https://docs.npmjs.com/misc/scripts)
