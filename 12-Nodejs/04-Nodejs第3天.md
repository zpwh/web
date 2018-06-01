# Node.js 第三天笔记

***

## 复习

### CommonJS 规范

- 一个文件就是一个模块
- 每一个模块都是一个单独的作用域
  + 也就是说在一个文件中定义的 变量、函数、对象等都属于当前模块内部私有的，外部是无法访问的
  + 不会污染全局作用域
- 每个文件模块对外接口是 `module.exports` 对象
  + 也就是说 `module.exports` 就是模块与模块之间通信的桥梁
- `require` 方法可以加载一个文件模块的 `module.exports` 接口
- 模块标识可以省略扩展名
- 模块可以多次加载，但是只会在第一次加载时运行一次，然后被缓存
- 模块都是同步加载的
  + 模块加载的顺序是按照代码中出现的顺序的

### Node.js 模块系统

- require 方法基本功能
  + 读入并执行一个 JavaScript 文件
  + 返回该文件模块的 module.exports 对象
  + 如果没有找到该模块，则报错

- require 方法查找加载规则
  + 优先从缓存加载
    * 无论是核心模块还是文件模块都会优先从缓存加载
  + 核心模块
    * 核心模块已经在把源码编译到了可执行的二进制文件中了
  + 以 `./` 或 `../` 开头的相对路径文件模块
    * 该相对路径是 相对于 require 方法所在的文件所属的目录的
  + 以 `/` 开头的绝对路径文件模块
    * 在 Windows 中， `/` 表示 require 方法所在文件所属的盘符，不要这样使用
    * 在 Linux 中，`/` 就表示 根路径
  + 加载一个目录
    * package.json 文件中的 main 属性
    * index.js index.node index.json
  + 加载一个包
    * module.paths
    * package.json
    * index.js index.node index.json
    * node_modules 目录一般用来放置第三方包的
    * 不要把自己写的模块或者包放到 node_modules 目录下

## npm

### 解决 npm 被墙的问题

- 第一种方式：通过指定镜像源地址来下载包：
`npm install 包名 --registry=https://registry.npm.taobao.org`

- 第二种方式：通过 淘宝提供的一个 cnpm 全局命令行工具
  + 安装全局命令行工具 `npm install -g cnpm`
  + 基本使用`cnpm install 包名`

- 第三种方式：通过一个全局命令行工具 `nrm` 来管理我们的镜像源地址
  + 安装nrm `npm install -g nrm`
  + 基本使用
    * 显示当前所有可用镜像源 `nrm ls`
    * 显示当前正在使用的镜像源 `nrm current`
    * 切换镜像源 `nrm use 镜像源名称`

## Node.js 的作用

### IO

### 输入与输出

### IO的不可预测性

## 异步编程

### 回调函数

将一个函数作为参数传递给另一个函数，并且通常在第一个函数执行完成后被调用

### 异常处理

- 处理异常的重要性
- try-catch 可以捕获同步代码出现的异常
- try-catch 无法捕获异步代码出现的异常
- 回调函数的设计
  + 第一个参数默认接收错误信息
  + 第二参数才是真正的结果
  + 强调错误优先

## 文件操作

### `path` 路径处理模块

- basename(path,[,ext])
- dirname(path)
- extname(path)
- isAbsolute(path)
- join([path1][,path2][,...])
- set

### `fs` 文件操作模块

- 同步和异步调用
- 文件写入
- 文件追加
- 文件读取
- 验证路径是否存在


### https://getlantern.org/ 翻墙软件
