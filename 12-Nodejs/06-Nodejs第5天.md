# Node.js 第五天课程笔记

***

## 1. Buffer

Buffer 是一个像 Array 的对象，主要用于操作二进制数据（字节）。

为什么要有Buffer？
计算机中存储的都是二进制数据

### 1.1 Buffer（二进制数据） 和字符串（字符）之间的的转换

在node最新的6.0版本（该版本对es6支持的程度达到了 93%）中，原生支持的字符编码如下：
- ascii
- utf8
- utf16le
- ucs2 他是 utf16le 的别名
- base64
- binary
- hex
- [官方文档链接](https://nodejs.org/dist/latest-v6.x/docs/api/buffer.html#buffer_buffers_and_character_encodings)

#### 1.1.1 Buffer转字符串

Buffer 对象的 `toString()` 方法可以将 Buffer 对象转换为字符串

- buf.toString([encoding[, start[, end]]])
  + encoding <String> Default: 'utf8'
  + start <Number> Default: 0
  + end <Number> Default: buffer.length

#### 1.1.2 字符串转Buffer

可以使用Buffer的构造函数：`new Buffer(str[, encoding])`，encoding 默认是 `utf8`，
官方已经不建议这么使用了。

在6.0.0中，官方建议使用：`Buffer.from(str[, encoding])`
- Buffer.from(str[, encoding])
  + str <String> String to encode.
  + encoding <String> Encoding to use, Default: 'utf8'

### 1.2 对于Buffer不支持的编码类型的解决方案

Node的Buffer对象支持的编码类型有限，
可以通过 `Buffer.isEncoding(encoding)` 来判断是否支持该编码，返回 `true` 表示支持

为了支持更多的字符编码类型，可以使用社区提供的 `iconv-lite` 包来解决。

iconv-lite 包的基本使用如下：

- 安装 `iconv-lite` 到当前项目中 
```
npm install iconv-lite
```

- 基本使用
```javascript
// 引包
var iconv = require('iconv-lite');
 
// 将一个 Buffer 对象按照 gbk 编码转换为字符串
str = iconv.decode(buf, 'gbk');
 
// 将一个字符串 按照 gbk 编码转换为 Buffer 对象
buf = iconv.encode("Sample input string", 'gbk');
 
// 检查 iconv-lite 包是否支持指定的编码
iconv.encodingExists("us-ascii")
```

## 2. path 路径处理模块

- basename(p[, ext])
- dirname(p)
- extname(p)
- isAbsolute(path)
- join([path1][, path2][, ...])
- parse(pathString)
- format(pathObject)
- path.sep
  + 在类 Unix 的操作系统上，路径分隔符是 `/`
  + 在Windows上，路径分隔符是 `\`

## 3. 文件操作

### 3.1 同步和异步文件调用 

### 3.2 文件相关操作

- 文件写入
- 文件追加
- 文件读取  
- 验证路径是否存在
- 获取文件信息
- 删除文件
- 重命名文件
- 移动文件
- 监视文件变化

### 3.3 目录相关操作

- 创建目录
- 重命名目录
- 读取目录
- 删除目录

### 3.4 命令行工具：项目初始化

#### 在 Windows 上配置全局命令行工具
 
1. 通过 npm root -g 可以查看当前全局命令行工具软化所在的目录
2. 例如：全局命令行工具目录是：C:\dev\nvm\npm\node_modules
3. 那么在 C:\dev\nvm\npm 该目录下随便找一个 后缀名是 .cmd  的文件
4. 复制一个副本出来
5. 然后将该文件改为你自己想要的命令行工具名
6. 右键 -> 编辑 *.cmd 文件
7. 在该文件中将 `"%~dp0\node.exe"  "%~dp0\node_modules\less\bin\lessc" %*` 改为  `"%~dp0\node.exe"  "%~dp0\node_modules\itcast\index.js" %*`
8. 该完之后，打开命令台，输入你刚才新建的那个 *.cmd 文件名 然后敲回车
9. 如果能看到里面的 index.js 中的代码被执行了，说明成功了

  
    
### 监视文件变化
 
#### 使用 browser-sync 浏览器同步刷新
[https://browsersync.io/docs/](官方网站)
1. 安装 `npm install --save-dev `
2. 在代码中使用

```
https://browsersync.io/docs/api/
var bs = require("browser-sync").create();

// 初始化开启一个服务，它会自动在浏览器中打开
bs.init({
    server: "./app"
});

// 手动刷新指定的页面，该文件必须属于 init 里面的 server 指定的根路径
bs.reload("*.html");
```


流在现实世界中是无处不在的。水流

### 3.5 文件流
## 网络编程

我们处于互联网时代，我们可以随时随地通过 Internet 上网、浏览新闻、玩LOL、上淘宝购物等等。
这些过程都发生了网络数据的交互。

简单来说：比如你正在手机上浏览网易新闻，对汪峰上头条很感兴趣，点击该链接后，就会进入新闻，
那么久会发生一件事：发出请求给网易服务器（告诉网易服务器我要查看汪峰上头条这条新闻），
服务器解析你的请求，返回汪峰头条新闻的具体内容。这个过程发生了数据的交换，
也就是请求数据传输给了网易服务器，网易服务器又返回响应数据给客户端

所以，网络编程 是指编写程序使两台联网的计算机可以完成网络数据交互，完成网络通信。
注意：这里的计算机泛指可以上网的设备，比如PC、手机、服务器、智能电视等等。

强调：网络编程重在思想，node只是一个可以帮助我们学习网络编程的一个工具而已。
使用其他编程语言或者操作系统进行网络编程，思想都是一样的。


### Socket

Socket 又叫做套接字，网络编程又叫做套接字编程。
而Socket 地址又称为 套接字地址，可以理解为计算机的网络地址。

假设你想和你的女神打电话，但是必须知道对方的电话号码才可以，
而我们进行网络通信也需要知道对方的 Socket 地址。

在网络通信中，采用类似方法标识Socket地址。
Socket地址最关键的两部分为（ip，port）
就是ip地址和端口号，
比如一个网络地址为 192.168.3.6:3000
那么，192.168.3.6 就是用来定位和区分计算机的
3000端口号就是用来区分不同的套接字的