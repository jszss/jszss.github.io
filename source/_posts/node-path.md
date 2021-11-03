---
title: 'node path'
date: 2021-01-27 10:06:19
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
console.log('*** app start ***');
console.log('***      module.filename = ' + module.filename + ' ***');
console.log('***           __filename = ' + __filename + ' ***');
console.log('***            __dirname = ' + __dirname + ' ***');
console.log('***        process.cwd() = ' + process.cwd() + ' ***');
console.log('*** require.main.filename= ' + require.main.filename + ' ***');
console.log('*** app end ***');

    module.filename：开发期间，该行代码所在的文件。
    __filename：始终等于 module.filename。
    __dirname：开发期间，该行代码所在的目录。
    process.cwd()：运行node的工作目录，可以使用  cd /d 修改工作目录。
    require.main.filename：用node命令启动的module的filename, 如 node xxx，这里的filename就是这个xxx。

    require()方法的坐标路径是：module.filename；fs.readFile()的坐标路径是：process.cwd()。
```
