# Node.js结合详解-process

## [Node.js](https://nodejs.org/en/)
整个脚手架工具的根本组成部分
使用到如下接口了：

## [`process`](http://nodejs.cn/api/process.html#process_event_exit) 进程
  - `process.exit()`事件: 显式调用 process.exit() 方法，使得 Node.js 进程即将结束

  - `process.cwd()`事件: 返回 Node.js 进程当前工作的目录，绝对路径，相当于`pwd`

  - `process.argv`属性，返回一个数组，这个数组包含了启动Node.js进程时的命令行参数。

## [`child_process.exec(command[, options][, callback])`](http://nodejs.cn/api/child_process.html#child_process_child_process_exec_command_options_callback)创建子进程

- 例子
```js
  const exec = require('child_process').exec
  const co = require('co')
  const prompt = require('co-prompt')
  const chalk = require('chalk')

  co(function *() {
    // 处理用户输入
    let projectName = yield prompt('Project name: ')
    let gitUrl = 'https://github.com/Wobugaosuni/react-redux-app-base.git'

    // git命令，远程拉取项目并自定义项目名
    let cmdString = `git clone ${gitUrl} ${projectName} && cd ${projectName} && rm -rf .git`

    // 终端白色字体输出
    console.log(chalk.white('\n Start generating...'))

    // 创建子进程
    exec(cmdString, (error, stdout, stderr) => {
      // 遇到错误，输入错误，结束进程
      if (error) {
        console.log(error)
        // 结束进程
        process.exit()
      }

      // 成功构建
      console.log(chalk.green('\n √ Generation completed!'))
      console.log(`\n cd ${projectName} && npm install \n`)
      process.exit()
    })
  })
```



