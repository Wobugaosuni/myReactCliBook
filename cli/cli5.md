# 5. 全局使用

1. 想让npm包全局安装后，能在电脑的命令栏里直接调用执行，需要在package.json里填写好"bin"这个字段:
```json
"bin": {
  "qiu": "bin/start"
},
```

2. 本地调试的时候，在根目录下执行:
`npm link`


