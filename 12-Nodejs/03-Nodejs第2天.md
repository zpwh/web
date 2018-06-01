# Node.js 第二天课程笔记
## 复习
### 基本使用
node文件路径+文件名

1. 控制台找到安装目录下的node.exe程序
2. 使用node.exe程序读取js脚本文件
3. 然后解析和执行 js 脚本文件

### 全局对象

- global
  + The top-level scope is not the global scope; var something inside an Node.js module will be local to that module.
- process
- console

### 全局函数

- setTimeout() 和 clearTimeout()
- setInterval() 和 clearInterval()
- setImmediate() 和 clearImmediate()

### 伪全局对象

- exports
- module
- require

### 伪全局变量

- __filename
- __dirname
## global
### process
进程：一个正在运行的程序

process：就是用来获取当前node运行进程的一些信息

当程序退出的时候，进程也就结束了

开发环境直接打印日志到控制台

生产环境不要打印了，把错误消息日志写入到文件中

如果是开发环境：NODE_ENV=develop

如果是生产环境：NODE_ENV=production

	var env = process.env['NODE_ENV'];
    console.log(env);
	if (env === 'develop'){
        console.log('开发环境');
    } else if(env === 'production'){
        console.log('生产环境');
    } 
获取对应的号结束进程

	var args = process.argv.slice(2);
	var pid = args[0];
	process.kill(pid);
process.mainModule

process.nextTick 异步的执行一个回调函数

console.log本身就是封装的下面的这段代码

- process.abort() 可以终止当前node进程
- process.arch  获取当前操作系统的 位数
- process.argv 可以获取用户通过命令台输入的参数
  + argv 是一个数组，数组中的第一项是 node.exe 可执行文件所在的绝对路径
  + argv 数组中的第二个参数就是当前执行文件的绝对路径
  + argv 中 从第二个元素开始才是 用户 输入的参数
  + 可以通过 `process.argv.slice(2)` 获取用户通过控制太传入的所有参数
- process.env 获取当前操作系统的用户变量 (了解)
  + 场景：开发的时候可以通过设置一些临时环境变量，用来区分是开发环境还是生产环境
  + 在Linux中可以这么做：`NODE_ENV=develop node example.js`
  + 在Windows中：`set NODE_ENV=production && node example.js`
- process.exit() 退出当前进程
- process.kill(pid) 通过输入一个进程号，用于结束一个进程
- process.nextTick(callback[, arg][, ...]) 可以异步的执行一个函数
- process.pid 获取当前进程的 进程id号
- process.platform  获取当前操作系统的所属平台

## 模块系统

### CommonJS 规范

### Node.js 基于 CommonJS 规范实现的模块系统

#### 基本使用

- 定义模块
  + 在CommonJS 规范中，一个文件就是一个模块
- 对外导出接口（exports 和 module.exports）
  + 
- 加载模块（require）


#### 核心模块

Node.js 默认提供了一些核心模块，实际上也是文件模块，
但是核心模块在源代码进行编译的时候已经被编译到了二进制的可执行文件中了

#### 文件模块

#### require 加载规则

- 优先从缓存中加载
- 不以 `./` 或 `../` 或 '/' 开头的核心模块
- 以 `/` 开头的 绝对路径文件模块
- 以 `./` 或者 `../` 开头的 文件模块
- 参数字符串可以省略扩展名

***

## 包 与 npm

### 包

#### 规范的包目录结构

#### 包的描述文件 package.json 文件

### npm

#### npm 开源库生态系统

#### npm 命令行模块管理工具




