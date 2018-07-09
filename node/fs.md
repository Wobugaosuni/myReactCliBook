# Node.js结合详解-fs

## [fs.statSync(path[, options])](http://nodejs.cn/api/fs.html#fs_fs_statsync_path_options)

```js
const fileName = '/Users/qiuxia/code/react/test'
fs.statSync(fileName)
```
返回：
```js
Stats {
  dev: 16777220,
  mode: 16877,
  nlink: 12,
  uid: 505,
  gid: 20,
  rdev: 0,
  blksize: 4096,
  ino: 139069065,
  size: 408,
  blocks: 0,
  atimeMs: 1530076744000,
  mtimeMs: 1530064892000,
  ctimeMs: 1530064892000,
  birthtimeMs: 1530064571000,
  atime: 2018-06-27T05:19:04.000Z,
  mtime: 2018-06-27T02:01:32.000Z,
  ctime: 2018-06-27T02:01:32.000Z,
  birthtime: 2018-06-27T01:56:11.000Z
}
```

## [stats.isDirectory()](http://nodejs.cn/api/fs.html#fs_stats_isdirectory)

如果 fs.Stats 对象表示一个文件系统目录，则返回 true 。
