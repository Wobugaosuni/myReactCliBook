# Node.js各种路径

`__dirname` `__filename` `process.cwd()` `process.argv`几种路径

## 举个例子

该项目的结构如下：
```
.
├── README.md
├── bin
│   └── start
├── command
│   ├── init.js
│   ├── page.js
│   └── test.js
├── package-lock.json
├── package.json
└── templates.json
```

其中，`package.json`中有一个`bin`字段
```json
"bin": {
  "qiu": "bin/start"
},
```

## 在该工程目录下执行

该项目工作目录为：
```bash
$ pwd
//输出： /Users/qiuxia/code/react/react-redux-app-cli
```

**`/bin/start`关于`test`的命令如下，在`react-redux-app-cli`目录下执行：**
```js
  'use strict'
  const commander = require('commander')

  // 定义脚手架的文件路径
  process.env.NODE_PATH = __dirname + '/../node_modules/'

  console.log('__dirname of start:', __dirname)
  console.log('process.env.NODE_PATH:', process.env.NODE_PATH)

  commander
    .command('test')
    .description('just test')
    .action(() => {  // 接收输入的参数
      require('../command/test')()
    })
```
输出如下：
```md
  /Users/qiuxia/code/react/react-redux-app-cli/bin
  /Users/qiuxia/code/react/react-redux-app-cli/bin/../node_modules/
```

**`/command/test.js`里代码如下，在`react-redux-app-cli`目录下执行：**
```js
  'use strict'
  const path = require('path')

  module.exports = () => {
    console.log('process.cwd():', process.cwd())
    console.log('process.argv:', process.argv)
    console.log('__dirname:', __dirname)
    console.log('__filename:', __filename)
    console.log('path.resolve(./):', path.resolve('./'))
  }
```
输出如下：
```md
/Users/qiuxia/code/react/react-redux-app-cli
[ '/Users/qiuxia/.nvm/versions/node/v8.11.2/bin/node', '/Users/qiuxia/.nvm/versions/node/v8.11.2/bin/qiu', 'test' ]
/Users/qiuxia/code/react/react-redux-app-cli/command
/Users/qiuxia/code/react/react-redux-app-cli/command/test.js
/Users/qiuxia/code/react/
```

## 在随便一个目录下执行

```bash
$ pwd
//输出： /Users/qiuxia/code/react
```

**`/bin/start`输出如下：**
```js
  console.log('__dirname of start:', __dirname)
  console.log('process.env.NODE_PATH:', process.env.NODE_PATH)
```
输出如下：
```md
/Users/qiuxia/code/react/react-redux-app-cli/bin
/Users/qiuxia/code/react/react-redux-app-cli/bin/../node_modules/
```

**`/command/test.js`输出如下：**
```js
  console.log('process.cwd():', process.cwd())
  console.log('process.argv:', process.argv)
  console.log('__dirname:', __dirname)
  console.log('__filename:', __filename)
  console.log('path.resolve(./):', path.resolve('./'))
```
输出如下：
```md
/Users/qiuxia/code/react
[ '/Users/qiuxia/.nvm/versions/node/v8.11.2/bin/node', '/Users/qiuxia/.nvm/versions/node/v8.11.2/bin/qiu', 'test' ]
/Users/qiuxia/code/react/react-redux-app-cli/command
/Users/qiuxia/code/react/react-redux-app-cli/command/test.js
/Users/qiuxia/code/react/
```

## 总结

- `process.cwd()`事件: 始终返回 **Node.js 进程当前工作的绝对目录路径**，相当于`pwd`

- `process.argv`属性，返回一个数组，这个数组包含了启动Node.js进程时的命令行参数。
第一个元素为`process.execPath`：始终返回**启动Node.js进程的可执行文件所在的绝对文件路径**，该文件是一个编译好的二进制可执行文件（程序）
第二个元素：始终返回**当前执行的符号链接的所在文件的绝对文件路径**。
剩余的元素为：其他命令行参数

- `__dirname`：始终返回命令行参数所在文件的**绝对目录路径**

- `__filename`： 始终返回命令行参数所在文件的**绝对文件路径**

