---
layout: post
title:  testcafe开发过程遇到的问题
category: JavaScript
tags: [testcafe]
---

## 问题1： 如何执行runner文件？
还没有package.json时方案：
1. 执行`npm link testcafe`
2. `node runner.js`
** 安装了package.json需要在package.json加上这句： `{"type": "module"}` **
原因看这里 ： https://stackoverflow.com/questions/45854169/how-can-i-use-an-es6-import-in-node
runner.js
```
import createTestCafe  from 'testcafe';

async function runner (){
 const testcafe = await createTestCafe('localhost', 1337, 1338);

 try {
     const runner = testcafe.createRunner();

     const failedCount = await runner
         .src(['test-demo.js'])
         .browsers(['chrome'])
         .run();

     console.log('Tests failed: ' + failedCount);
 }
 finally {
     await testcafe.close();
 }
}
runner ();
```

## 问题2： 如何管理包？ node module
`npm init`  
生成package.json文档
```
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "cart-wrapper.js",
  "dependencies": {
    "testcafe": "^1.9.2"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

```

## 问题3： ESlint 如何使用？
1. 安装
`npm install -g eslint` 全局安装
`eslint init` 初始化文档
2. 使用
`eslint ./`
到这里出现 一个新问题，由于为了解决问题1，在package.json加上这句： `{"type": "module"}`，导致eslint 报错，这里使用的是 `.eslintrc.js`文档，报错改为`.eslintrc.cjs`后正常

## 问题4： npm切换国内源
`npm config set registry http://registry.npm.taobao.org`

## 问题5： 多个js文件共用fixtrue
`helper.js` 文件中写一个方法，如下：
```
export function openShopFixture(){
    fixture `Open Shop`
        .page `${website_url}${url["shop"]}`;
}
```
在测试用例前调用即可
```
import * as help from '../helper';
help.openShopFixture();
```

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
