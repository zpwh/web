# Node.js 第7天课程笔记
createServer方法的第一个参数可以传递一个函数，默认监听connection事件
IP地址用来定位一台计算机的，而端口号是用来定义一个具体的应用程序的
当server.listen
监听和客户端通信的Socket的error事件
例如：当客户端强制关闭的时候就会导致服务器异常
只要error事件被触发
## 复习网络编程

重在思想，node只是一个用来辅助学习网络编程的工具而已。
我们自己定义格式的目的其实就是在定义服务器和客户端之间的一种通信约定，通信规范而这个约定或者说是规范 就是协议
我们使用json作为客户端和服务器通信的一种交互数据格式
1. 客户端连接服务器

node会自动给客户端分配一个端口号用来与服务器
- 什么是网络编程
- 使用 node 进行网络编程需要使用其它web服务器作为容器吗
- 什么是协议？
- 在网络编程中，为什么要有协议？制定协议有什么好处？
- 什么是 Socket？
  + ip
  + port

### net 模块的基本使用

net模块提供了一个异步网络包装器。
该模块中包含了一些方法用于创建服务器和客户端。
在使用 net 模块的时候，需要单独的 `require('net')`。

### 服务器端相关操作API

- net.createServer([options][, connectionListener])
- listening：调用 server.listen() 绑定端口之后会触发
- connection：每个客户端套接字连接到服务器时触发
- close：当服务器关闭时会触发，只有手动调用 server.close() 之后会触发该事件
- error：当服务器发生异常的时候，会触发该事件
- server.address()
- server.close([callback])
- server.getConnections(callback)
- server.listen(port[, hostname][, backlog][, callback])

#### Socket相关操作API

- socket.connect(options[, connectListener])
- socket.connect(port[, host][, connectListener])
- data 当一端调用 write() 方法发送数据时，另一端就会触发 data 事件，事件回调处理函数中的参数就是 write() 发送的数据
- end 当连接中的任意一端发送了 FIN 数据时，将会触发该事件
- connect 该事件用于客户端，当套接字与服务器连接成功时会被触发
- error：当异常发生时，触发该事件
- close：当套接字完全关闭时，触发该事件
- socket.address()
  + `{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`
- socket.remoteAddress
- socket.remotePort
- socket.setEncoding([encoding])
- socket.write(data[, encoding][, callback])

## http协议

HTTP协议就是 浏览器 和 服务器 之间通信的一个数据格式规范

在HTTP协议中，始终是以一种 一问一答 的形式在进行沟通和交流（数据交换）

服务器如果没有收到浏览器的请求消息，服务器永远不会主动的发送响应消息

浏览器不发出请求，服务器不会主动的发送响应

- 浏览器发送请求数据到服务器
- 服务器解析浏览器发送的请求数据
- 服务器响应数据到客户端浏览器

### B/S 网络架构

通常我们所说的 Web 开始就是一种 B（Browser）/S（Server） 结构开发模型

也就是 浏览器和服务器 交互模型



### 在地址栏输入网址后页面是如何呈现的？

- 输入 URL：http://www.baidu.com
- DNS 域名解析
  + 计算机无法识别域名，计算机与计算机之间要想进行通信，必须通过ip地址用来定位该计算机所在的位置
  + 在浏览器中，输入的ip地址或者域名，默认给你加了一个80端口号（对方的服务器监听的就是80端口）
  + 158.12.25.652  域名就是为了好记
  + 为了好记，所以我们的 万维网提供了一个域名这样的概念
  + 当你输入了 ip 地址后，浏览器会自动去找DNS域名解析服务器，
- 建立 TCP 连接（Socket）：三次握手
- 将用户输入的地址封装成 HTTP Request 请求报文 发送到服务器
  + 浏览器将用户输入的 URL 地址根据HTTP协议 封装成了  http 请求报文（请求头+请求行+请求体）
  + 该报文说白了也就是字符串而已，最终也要被转成了二进制数据再发送到服务器
- 后台服务器接收到用户HTTP Request 请求报文
  + 后台服务器接收到 客户端发送给自己的数据（二进制数据）
    * 首先把二进制数据按照编码解析成字符，（人类可以识别的）
    * 解析成字符之后，再按照 HTTP 协议规范中定义的格式解析出来
- 后台服务器处理用户请求信息
  + 当得到用户请求报文之后，根据请求报文中的 get、port或者 URL、或者URL中的查询字符串或者 请求体中的数据
  + 根据用户的特定的请求数据做特定的处理
- 后台服务器将相应结果封装到 HTTP Response 响应报文中 发送给客户端
  + 当我们解析和处理完用户请求报文消息之后
  + 服务器开始将具体的 要发送给客户端的数据 根据 HTTP 协议规范 封装成 HTTP协议响应报文
  + 响应头、响应字段、响应体
  + 该数据说白了也是具有特定格式的字符串而已，最终这个字符串也要转换成二进制数据发送到客户端
  + 发送到客户端也是通过 Socket（ip地址、端口号） 发送到了该客户单
- 用户浏览器接收到响应后开始渲染html、css，解析和执行 JavaScript 代码
  + 当客户端解析到 服务器发送过来的 二进制数据
  + 客户端浏览器也会将 二进制数据 根据编码类型解析成 字符串
  + 然后根据 HTTP 协议，解析服务器发送过来的 响应报文
  + 然后根据响应报文中的报文内容（报文头、报文体）做具体的解析
- 当浏览器在解析的过程中遇到 一些静态资源时，会再次重复上面的步骤
 

## 使用 http 模块进行web开发

创建 HTTP 服务器

`http.createServer([requestListener])`

服务器相关操作事件和API

- Event: 'close'
- Event: 'connection'
- Event: 'request'
- server.close([callback])
- server.listen(port[, hostname][, backlog][, callback])

请求对象
- Event: 'data'
- message.headers
- message.httpVersion
- message.method
- message.url
  + require('url').parse(request.url)
  + require('url').parse(request.url, true)

响应对象
- response.end([data][, encoding][, callback])
- response.setHeader(name, value)
- response.statusCode
- response.statusMessage
- response.write(chunk[, encoding][, callback])
- response.writeHead(statusCode[, statusMessage][, headers])

## 有关ajax的部分网站

1. [微信](http://mp.weixin.qq.com/wiki/11/74ad127cc054f6b80759c40f77ec03db.html)
2. [网址1](http://www.uploadify.com/documentation/)
3. [网址2](http://odyniec.net/projects/imgareaselect/)
4. [网址3](http://plugins.jquery.com/form/)
