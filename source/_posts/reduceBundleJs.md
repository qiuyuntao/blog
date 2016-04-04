---
title: 减少bundle.js体积
date: 2016-04-04 12:12:57
tags: javascript
---

[本文为译文，原文点我](https://lacke.mn/reduce-your-bundle-js-file-size/)

我开发了很多年的SPA（单页应用），然而我总是很惊讶很多开发者都不去思考`bundle.js`的体积大小。

> “压缩代码之后，大小还是可以接受的啊” ~一些人是这么说的，但是现在我不这么认为

即使我压缩`bundle.js`，在一个大型的应用中也会花费很多时间去加载这些资源，在低网速和手机上显示的时候特别慢。我们怎么样才能显著的解决这个问题呢？

非常简单！使用相对的文件路径。让我们来看下这个例子，看看有什么不同。


#### 例子1

首先，我们用ES6的解构语法加载模块来编写一个简单的应用。

```js
# src/example.js

import { concat, sortBy, map, sample } from 'lodash';

// Example: sortBy
const users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 42 },
  { 'user': 'barney', 'age': 34 }
];
const exampleSortBy = sortBy(users, function(o) { return o.user; });
console.log(exampleSortBy);

// Example: map
const exampleMap = map(users, 'user');
console.log(exampleMap);

// Example: concat
const array = [1];
const exampleConcat = concat(array, 2, [3], [[4]]);
console.log(exampleConcat);

// Example: sample
const exampleSample = sample([1, 2, 3, 4]);
console.log(exampleSample);
```

我们使用`browserify`来编译、打包这个应用

`browserify src/example.js -o dist/bundle.js -t [ babelify --presets [ es2015 ] ] -v -d -g uglifyify `

目前为止，情况很好。我们编写下一个例子，然后比较一下编译打包后的文件大小。

#### 例子2

我们编写一个功能一样的应用。但是我们使用文件的路径来加载所有的模块，而不使用ES6的解构来加载模块。

```js
# src/example-2.js

import concat from 'lodash/concat';
import sortBy from 'lodash/sortBy';
import map from 'lodash/map';
import sample from 'lodash/sample';

// Example: sortBy
const users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 42 },
  { 'user': 'barney', 'age': 34 }
];
const exampleSortBy = sortBy(users, function(o) { return o.user; });
console.log(exampleSortBy);

// Example: map
const exampleMap = map(users, 'user');
console.log(exampleMap);

// Example: concat
const array = [1];
const exampleConcat = concat(array, 2, [3], [[4]]);
console.log(exampleConcat);

// Example: sample
const exampleSample = sample([1, 2, 3, 4]);
console.log(exampleSample);
```

现在，我们来编译我们的代码

`browserify src/example-2.js -o dist/bundle-2.js -t [ babelify --presets [ es2015 ] ] -v -d -g uglifyify `

** 问题 **：你觉得哪个例子生成出来的文件更小？

#### 比较

我们的应用做的事情完全一样。代码也几乎相同，编译之后我们发现例子2的代码要小很多。

```
$ ls -lha dist/
bundle-2.js (84K)
bundle.js (204K)
```

原因我们在上面已经提到了：我们没有引入所有`lodash`,而是引入了我们需要用的文件。

这个对于所有的`node modules`都适用。简单的把引入模块的结构语法替换成实际路径引入的语法，很快能到减少的文件大小。

#### 源码
如果你想看这个例子的源码，你可以从github上check out 这个仓库

https://github.com/tlackemann/minimize-bundle-js-size

我收到了很多回复提到了Webpack2、Rollup等等。是的，这些新技术是很棒，有一个名为`tree shaking`的功能（可以在打包中不引入我们不需要的代码）。但是在你接手一个老的项目的时候，你很有可能是不能使用这些新技术，需要的是一些其他的办法来解决这个问题。本文提到的方法可以更快速的解决你当前遇到的问题。
