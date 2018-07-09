# 3. 入口文件

1. 建立项目：`npm init`

2. 安装相关依赖
`npm i chalk co co-prompt commander metalsmith handlebars glob -S`

3. node内置了对命令行操作的支持，node工程下的`package.json`中的`bin`字段可以定义命令名和关联的执行文件
```json
  "bin": {
    "qiu": "bin/start"
  },
```

4. 在根目录下新建入口文件`/bin/start`
文件内容：
```js
  #!/usr/bin/env node --harmony
  'use strict'
  const commander = require('commander')

  // 定义脚手架的文件路径
  process.env.NODE_PATH = __dirname + '/../node_modules/'

  // 定义当前版本
  commander
    .version(require('../package').version )

  // 定义使用方法
  commander
      .usage('<command>')

  // 定义脚手架支持用户输入的命令
  // 初始化项目
  commander
      .command('init')
      .description('Generate a new project')
    .alias('i')
    .action(() => {
      require('../command/init')()
    })

  // 处理参数
  commander.parse(process.argv)

  // 提供帮助信息
  if(!commander.args.length){
    commander.help()
  }
```
写完后在终端执行`node start`，可以看到相应输出
