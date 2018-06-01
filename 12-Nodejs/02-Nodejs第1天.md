# Node.js 第一天课程笔记

## 模块化开发复习 

### 什么是模块化

- 现实中的模块化
  + 就是一种生产的方式而已
  + 生产效率高
  + 维护方便，成本低
- 程序中的模块化
  + 就是开发方式而已（代码的编写和组织方式）
  + 开发效率高
  + 方便维护了（维护的成本更低）

- 为什么要在 程序 中使用 模块化的开发方式
  + 命名冲突
  + 文件依赖

### `SeaJS` 的使用

- 定义模块 `define`
- 定义模块 `define`
- 的撒打算大大萨啊的撒按时撒
- 加载模块 `require`
  + 在一个模块系统中，`require` 加载过的模块会被缓存
  + 默认 `require` 是同步加载模块的
  + 可以通过 `require.async('模块标识',callback)` 使用异步的方式加载一个模块
- 暴露接口 `exports` 和 `module.exports`
- 启动模块系统 `seajs.use(callback)`
  + seajs.use 和 Document 的 ready 没有任何关系
  + 要想保证 文档结构加载完毕再执行你的 js 代码，一定要在 seajs.use  内部通过 window.onload 或者 $(function(){})

- 分清楚前台模块化和node中的模块化的区别

- 掌握模块化的思想

## Node 简介

### PHP 是世界上最好的语言吗？

```
$a
$b
echo
```

### JavaScript 是世界上最好的语言？

JavaScript并不一定是世界上最好的语言，但是一定是最流行的语言

### 客户端 JavaScript 是怎样的？

- 什么是客户端
  + 面向用户的端就是客户端
  + 和服务器端是对立的：提供服务的

- 什么是 JavaScript？
  + 一种语言
  + 若类型
  + 脚本语言（不需要预编译的语言）
    * 计算机只能识别 0 和 1  ，也就是二进制代码
    * 脚本语言就是不需要提前编译，而是在*运行时动态的编译和解析执行*
    * 脚本语言也叫作 动态语言
    * 还有一种语言叫作：静态语言（静态语言需要经过编译之后才能执行）
  + 运行在浏览器中
  + JavaScript 就是一种运行在 浏览器 中的 脚本语言
- JavaScript 是运行环境是什么？
  + 浏览器
  + 理论意义上，JavaScript 是运行在 浏览器中的 js 解析引擎中
- 浏览器中的 JavaScript 可以做什么？
  + 从 JavaScript 语言角度来说：if else var while for switch [] {} function
  + 理论意义上的js  是指  ECMAScript 3（JavaScript 语言标准规范）
  + DOM操作
  + window  document onclik  onmousemove 它们都是 浏览器 开放给 程序员的 接口
  + ajax 编程  var xhr = new XMLHTTPRequest();
  + 事件驱动编程
  + 使用 JavaScript 语言 在浏览器中做界面交互和基本的程序逻辑（表单校验）
- 浏览器中的 JavaScript 不可以做什么？
  + 相对于 传统的 c、Java、c#、c++ 等等这些语言来说
  + 文件操作
    * 注意：JavaScript 本身不是不可以操作文件
    * 为了 安全性
  + 客户端的 JavaScript 可以向 服务器 发送请求
  + 客户端 JavaScript 只能发送请求，而不能接收请求
- 在开发人员能力相同的情况下编程语言的能力取决于什么？
  + 最重要的一个区别
  + 最重要的区别 取决于 你的 执行环境
  + 一些后台语言：Java、PHP、c#、c++ 运行环境不一样
  + 编程语言的能力 真正 取决于 这个语言在哪儿运行（运行环境）
- JavaScript 只可以运行在浏览器中吗？
  + JavaScript 不仅仅能够运行在浏览器中？
    * 汽车中的发动机
    * 引擎最重要的特定：可移植
- Chrome 浏览器的实现结构

### 什么是 Node?

- [https://nodejs.org/en/]()
- Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. 
  + JavaScript runtime  JavaScript 运行时
  + Chrome's V8 JavaScript engine Chrome 浏览器 V8 引擎
  + Node.js 是一个 构建于 谷歌的 Chrome 浏览器的 V8 引擎之上的一个 `JavaScript运行时` 环境
  + Node.js可以解析和执行 JavaScript 代码
- Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. 
  + event-driven  事件驱动模型
  + non-blocking I/O model  非阻塞IO模型  IO（input/output）输入与输出
  + lightweight[ˈlaɪtweɪt]  轻量级
    * 在软件开发行业中，轻量级标识褒义词
    * 轻量级也就意味着 运行速度快
    * 轻量级也就意味着有更好的 跨平台 特性（平台的差异性，兼容性）
  + efficient[ɪˈfɪʃnt] 高效的
  + Node.js的 事件驱动和非阻塞IO模型使得Node.js本身非常的轻量和高效
- Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
  + package ecosystem npm  包生态系统 npm
  + largest  最大的
  + open source libraries 开源库
    * 理论意义上 开源就表示有成熟的社区，开放源代码
  + Node.js 的npm包生态系统，是世界上 最大的 开源库 生态系统
  + 以前的 客户端中 JavaScript 库 散列在互联网的各个地方
  + npm 就是 把大家经常使用的一些开源库 给 组织到了一起

Node 是一个可以解析和执行 JavaScript 代码的 运行时环境

- Node.js 的作者叫什么？
  + 瑞恩.达尔

- Node.js 是 JavaScript 吗？
  + Node.js 不是 JavaScript ， Node.js 不是一种 语言
  + Node.js 不是 框架、库
  + Node.js 是一个可以解析和执行 JavaScript 代码的一个运行时环境


JavaScript语言在服务器端的运行环境

1. JavaScript语言通过Node在服务器运行，在这个意义上，Node有点像Java虚拟机
2. Node提供大量工具库，使得JavaScript

### Chrome 浏览器的实现结构

- Webkit 渲染、布局引擎
- V8 JavaScript 解析执行引擎   语言本身指  ECMAScript
- 中间层（DOM、BOM） 浏览器暴露出来的接口
- 硬件层

### Node 的实现结构
- V8 JavaScript 解析执行引擎   ECMAScript
- 中间层 （提供了文件操作、网络操作登陆接口）更加接近操作系统的接口供开发人员使用
- 硬件层


### Node 可以做什么

- 操作文件（创建、删除、修改、读取）
- 提供Web服务（在Node中可以接收客户端的请求了）
- Node 可以 开发一些 命令行工具软件
- Node 可以 开发动态网站（有用户业务交互的功能Web站点）
  + 用户登陆
  + 用户注册
  + 添加购物车
  + 商品的展示
- Node 可以帮我们 把之前 所写的 静态页面  -> 动态化
- Node.js 再也不需要操作DOM、BOM了，再也不需要写HTML、css 不需要关系 兼容性的问题
- Node.js 编程实际上就是在 写 JavaScript 代码，关心的是业务功能
- 操作持久化数据
- 可以开发 命令台 工具软件

### Node.js 和 PHP 有什么区别？

- 它们都能操作文件，都有和操作系统底层打交道的 API
- 它们都可以进行网络操作，网络服务
- PHP 需要和 Apache 结合起来才能提供 Web服务
- Node.js 摒弃了以往所有的 服务器
  + Node.js 可以独立作为一个服务器来使用
- Java、PHP、.net 能做的事儿，Node.js 基本都能做，而且在某一方面比它们还要做的好

### 谁在使用 Node

国内一些创业公司用用的比较多，功夫熊（做上门保健的，美甲、按摩）
国外的一些大公司都有使用：Facebook、Twitter、Google
国内的一些大公司：Alibaba（天猫所有的页面都是通过Node提供的服务）、Tencent、Baidu

### 如何学习 Node

- 阅读一些大牛写的技术博客
- 看一些大牛写到书
  + 深入浅出Node.js（作者：Alibaba：朴灵）学完Node.js之后，甚至使用Node.js工作了半年了再看
- 多写代码



## 安装与配置

### 安装包的方式安装

- 下载地址：
- 一路下一步 next
- 如何确认是否安装成功：
  + `win + r` ，然后输入 `cmd` ，然后敲回车 就可以进入 cmd 控制台

### nvm 安装和管理我们的 Node.js版本
## 控制台基本使用cmd
1. cmd ：command 命令行程序，允许用户可以在终端台中与操作系统交互其实就是输入与输出（输入一些命令，输出一些结果）
2. 作用：输入一些命令， cmd.exe 可以执行，
3. 在cmd 中操作文件目录
	1. cd （change directory） 切换目录
	2. mkdir/md （make directory ） 创建一个文件夹
	3. rd （remove directory） 删除文件夹
	4. del （delete ） 删除指定文件
	5. dir 列出当前目录中所有的内容
	6. ren （rename ） 改变文件名
	7. cls|clear （clear screen） 清屏
## 控制台基本使用

允许用户可以在终端命令台中与操作系统交互，其实就是输入与输出

### 如何打开cmd

1. 通过 按 window 键，输入 `cmd` 打开cmd程序
2. 通过 `win+r`  输入 `cmd`，敲回车就可以进入

### 基本命令

- `dir` directory 列出当前目录下所有的条目
  + 别名 `ls` 在 powershell 中可以使用
- `cd` change directory 切换目录

```
切换到当前目录下的 Desktop 目录
当想切换到当前目录的时候，最好使用 cd ./ 相对路径的形式
C:\Users\iroc>cd Desktop
C:\Users\iroc\Desktop>

在Windows 上切换盘符：
`d:`

切换绝对路径之后再同一个盘符下才有效

切换到上一级目录
C:\Users\iroc\Desktop\code\seajs>cd ../
C:\Users\iroc\Desktop\code>

连续进入多级目录
C:\Users\iroc\Desktop\code>cd seajs/a
C:\Users\iroc\Desktop\code\seajs\a>
```

- `cls` clear screen 清屏
  + 别名 clear 在widnows中的 `powershell` 中可以使用

### path 环境变量

目的是为了在控制台中的任何目录都可以快速打开或者使用该可执行文件

环境变量就是用来存储系统级别的变量

- 添加环境变量
  + 我的电脑 -> 右键选择属性 -> 高级系统设置 -> 切换到`高级`面板 -> 环境变量
  + 第一种方式：直接把可执行文件所属的目录 放到 PATH 环境变量中（如果没有PATH环境变量，自己新建）
  + 第二种方式：新建一个环境变量，变量名规范：逻辑名_HOME 变量值：该可执行文件所属的目录
  + 注意：无论是直接添加的路径还是引用的变量名，一定要用 英文的分号 区分开
  + 引用变量名的时候，变量名两边都是 `%`

`> feiq`
当你在控制台中输入一个程序的名字的时候，cmd 默认把它当成一个可执行文件去执行了，优先找当前目录下是否有没有一个叫做feiq.exe 的可执行文件，如果有，直接执行打开如果没有，cmd会进入 path 环境变量中 一个目录一个目录的挨着查找里面是否有该可执行文件

## REPL(Read-eval-print-loop) 运行环境

就是浏览器中的控制台，可以辅助我们做一些API测试

- 通过在控制台中输入 `node` 敲回车就可以计入 REPL 运行环境
- 通过在REPL运行环境中 连续按两次 `Ctrl+C` 就可以退出 REPL 运行环境

1. 作用
	1. 方便测试JavaScript代码的运行环境
2. REPL基本操作
    1. 变量、函数、对象
    2. 直接运行函数
    3. 使用下划线字符，表示上一个命令的返回结果
3. REPL基本命令
	1. .help  .exit

## Global

### __dirname 和 __filename

它们属于模块作用域，可以直接使用
它们两个用来获取路径的，一般用于操作文件路径的时候，才会用到

## process

process 是一个全局可用对象，可以在任何地方使用

- process.argv
  + 可以通过该属性，获取命令台输入的一些参数

## 模块系统

## 包

## npm

