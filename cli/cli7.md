# 7. 发布到NPM

1. 将本文的脚手架代码放到github

2. 终端注册/登录npm
```
npm adduser  //如果没有账号，用此命令注册
npm login   //如果有账号，用此命令登陆
```

3. 到npm官网查询发布的脚手架名称是否有重复（不允许重名）
脚手架名称是根据`package.json`的`name`字段定义的

4. 发布
`npm publish`
