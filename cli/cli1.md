# 1. 技术选型

## [Node.js](https://nodejs.org/en/)

整个脚手架工具的根本组成部分
使用到如下接口了：

- **[`process`](http://nodejs.cn/api/process.html#process_event_exit) 进程**
  - `process.exit()`事件: 显式调用 process.exit() 方法，使得 Node.js 进程即将结束

  - `process.cwd()`事件: 返回 Node.js 进程当前工作的目录，相当于pwd目录

  - `process.argv`属性，返回一个数组，这个数组包含了启动Node.js进程时的命令行参数。
  第一个元素为`process.execPath`。返回启动Node.js进程的可执行文件所在的绝对路径。如`'/usr/local/bin/node'`
  第二个元素为当前执行的JS的文件路径。
  剩余的元素为其他命令行参数

- **[`child_process.exec(command[, options][, callback])`](http://nodejs.cn/api/child_process.html#child_process_child_process_exec_command_options_callback)创建子进程**

- 例子
```js
  const exec = require('child_process').exec
  const co = require('co')
  const prompt = require('co-prompt')

  co(function *() {
    // 处理用户输入
    let projectName = yield prompt('Project name: ')
    let gitUrl = 'https://github.com/Wobugaosuni/react-redux-app-base.git'

    // git命令，远程拉取项目并自定义项目名
    let cmdString = `git clone ${gitUrl} ${projectName} && cd ${projectName} && rm -rf .git`

    // 创建子进程
    exec(cmdString, (error, stdout, stderr) => {
      // 遇到错误，输入错误，结束进程
      if (error) {
        console.log(error)
        // 结束进程
        process.exit()
      }

      // 成功构建
      process.exit()
    })
  })
```

## [ES6](http://es6.ruanyifeng.com/)

新版本的node.js对于es6的支持度已经非常高

## [Commander](https://github.com/tj/commander.js/)命令行工具

想让程序能够接收用户输入的指令,可以使用此工具。能够更好地组织和处理命令行的输入

## [co](https://github.com/tj/co)
异步流程控制工具

## [co-prompt](https://github.com/tj/co-prompt)

自动提供提示信息，并且分步接收用户的输入，体验类似`npm init`时的一步一步输入参数的过程
```js
  var name = yield prompt('username: ');
```

## [metalsmith](https://github.com/segmentio/metalsmith)

是一个静态模板生成器，根据官方的介绍：
> An extremely simple, pluggable static site generator.

类似的还有Hexo等

在此项目中，利用`metalsmith`和`handlebars`的结合。将用户输入的变量插入到模板中

## [handlebars](http://handlebarsjs.com/)

是模板引擎，类似的还有pug(jade)、ejs
语法很简单，就是用双括号把变量包起来
```html
<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{body}}
  </div>
</div>
```

## [glob](https://github.com/isaacs/node-glob)

筛选和返回文件夹下的所有文件，是一个array
```js
// 遍历当前目录
const list = glob.sync('*')
```
返回：
```js
[ 'create-react-app',
  'hwxyz',
  'react-course',
  'react-redux-app-base',
  'react-redux-app-cli',
  'sellByReact',
  '搭建react项目(webpack)' ]
```

## [chalk](https://github.com/chalk/chalk)

美化终端输出，给枯燥的终端加上点颜色
```js
  const chalk = require('chalk');

  // 用蓝色输出
  console.log(chalk.blue('Hello world!'));
```


