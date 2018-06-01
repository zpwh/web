# Node.js 第四天课程笔记
## 1. 复习
### 1.1 异步编程
同步编程：符合程序员的逻辑思维
异步编程方式：在JavaScript中会经常遇到：

	$.ajax({
	  url:'',
	  success: function(data){
	    // "{ "name": "jack" }"
	    // 该异步操作需要上一步异步操作返回来的数据
	    $.ajax({
	      url: '',
	      data: data,
	      success: function(data){
	        $.ajax({ url: '', data: '', success: function() {} })
	      }
	    });
	  }
	});
#### 1.1.1 回调函数

将一个函数作为参数传递给另一个函数，并且通常在第一个函数执行完成后被调用

因为第一个函数的执行不确定什么时候执行结束

#### 定时器
	// 在 js 中，定时器不一定准确
	// 在 js 中，console 提供了一个方法 time timeEnd
	// time 和 timeEnd 通常用来统计一段代码的执行时间
	// time 和 timeEnd 方法需要一个参数，对于同一段业务逻辑代码来说，该参数必须一致
	// 要想在一个脚本文件中使用多次，必须使用参数 戳 来标记
	// console.time('timer');
	// for( var i = 0; i< 100000000; i++ ){
	
	// }
	// console.timeEnd('timer'); // timer: 113.024ms

#### 1.1.2 异常处理
- try-catch 捕获异常
- 回调函数的设计
  + 回调函数一定作为参数的最后一个参数出现
  + 第一个参数默认接收错误信息
  + 第二个参数才是真正的数据

## 2. node 调试

### 2.1 console.log

`console.log` 是最方便的，也是最快的。

### 2.2 node内置调试器（不推荐使用）

使用方式：在控制台中输入以下命令：
```
node debug 脚本文件名
```

执行上面的命令结束之后，代码会自动停在脚本的第一行，等待用户执行其它调试命令。
可以通过输入 `help` 命令查看可用命令

### 2.3 node-inspector

node-inspector 是一个第三方全局命令行调试工具。
[node-inspector](https://github.com/node-inspector/node-inspector)

#### 2.3.1 安装

```
npm install -g node-inspector
```

#### 2.3.2 启动调试

```
node-debug app.js
```

`node-debug` 命令会自动在当前操作系统默认浏览器中加载node调试器

默认情况下，代码会快速执行结束，
所要想让代码停留在程序的第一行位置，可以输入下面的命令启动调试：

```
node --debug-brk app.js
```

这样的话，调试器启动只有会自动停留在程序的第一行位置等待输入命令进行后续调试操作。

调试的快捷键和在 `Chrome` 浏览器中的快捷键是一样的

### 2.4 visual studio code 调试 node

[visuao studio code 官方网站](https://code.visualstudio.com/)

#### 下载

[visuao studio code 下载地址](https://code.visualstudio.com/Docs/?dv=win)

#### 安装

手动安装，一直下一步下一步就可以了

#### 开始调试

[vsc官方文档调试链接](https://code.visualstudio.com/docs/editor/debugging)

1. 必须以项目的方式打开要调试的js脚本所在的目录，目录路径最好不要包含中文，否则可能有问题
2. 在要调试的脚本文件中，找到具体要设置断点的行，在左侧点击设置断点
3. 设置好断点之后，按`F5`启动调试
4. 这个时候，`vsc` 编辑器会提示你选择要调试的环境，这里选择 `Node.js` 即可
5. 当选择完调试环境之后，`vsc` 默认会在当前根目录下生成一个 `.vsccode` 目录
6. 在 `.vsccode` 目录下找到一个叫做 `launch.json` 的文件，打开编辑
7. 在 `launch.json` 文件中，在 `configurations` 节点下找到一个叫做 `program` 的属性节点
8. 将 `program` 属性节点中原来的值 `${workspaceRoot}/app.js` 改为 `${workspaceRoot}/要调试的脚本文件名.js`
9. 修改完毕之后，按 `Ctrl+F5` 保存
10. 上述操作完成之后，按 `F5` 启动调试
11. 尽情的享受 `vsc` 调试带给你的调试的乐趣吧
12. 快捷键和 `Chrome` 浏览器中的调试环境快捷键一致

对于执行了以上操作还没有成功的同学，建议将 `vsc` 关闭重新打开再次按 `F5` 启动调试即可解决

### 2.5 webstorm 调试 node

#### 开始调试

1. 在要调试的文件中具体的行位置左边通过 `Ctrl+F8` 设置一个端点
2. 在当前要调试的文件中通过鼠标右键，然后选择 `Debug 要调试的文件名.js`
3. 这个时候 ws 会自动帮你启动调试模式，并且自动停留在你打击端点的位置
4. `F8` 步进
5. `Shift + F8` 步出
6. `Alt + F8` 可以执行一个表达式
7. `Ctrl + F5` 重新启动调试

## 3. ECMAScript 2015

ECMAScript 是当前 JavaScript 语言规范的最新标准，一般称为 es6，
但是因为 该标准规范是在 2015年6月份发布的，所以也叫作 ECMAScript 2015

目前 ECMAScript 2016 标准的指定也在规划中，ECMAScript 2017 也在制定中了，已经有了一些阶段
stage-1 stage-2 stage-3 stage-4

### 3.1 严格模式

要想使用　ES 2015 ，一定要开启 严格模式

开启严格默模式：`"use strict;"`

### 3.2 let 变量声明

es2015 中新增了一种变量声明的方式： `let`，类似于 `var`,
通过 `let` 声明的变量只在 `let` 命令所在代码块内有效。

块级作用域，块级其实就花括号之间的代码自动形成一个单独的作用域

- 为什么要有块级作用域？
  + 内层变量可能会覆盖外层变量
  + 用来计数的循环变量泄露为全局变量

使用 `let` 注意事项：
- 不存在变量提升，变量一定要先声明，后使用，否则报错
- 在相同作用域内，不允许重复声明同名变量，否则报错
- 块级作用域
  + 外层代码块不受内层代码块的影响
  + 外层作用域无法读取内层作用域的变量
  + 内层作用域可以定义外层作用域的同名变量

使用场景：
一般在块内部使用 let 变量进行声明

### 3.3 const

`const` 也是用来声明变量，但是声明的是常量。一旦声明，常量的 `值` 不可改变

使用 `const` 注意事项：
- 通过 `const` 声明常量的同时必须初始化赋值，否则报错
- 一旦声明，常量的值不可改变，否则报错
- `const` 也是块级作用域，只在声明所在的块级作用域内有效，不建议在 块内使用 const
- 不存在变量提升
- 不可重复声明

`cosnt` 使用场景：

所有不希望用户去改变的变量就通过 `const` 声明为常量

	const fs = require('fs');
	const os = require('os');
通过 `const` 声明的常量不可改变的是常量的地址，如果该常量是一个对象，依然是可以被修改的

	'use strict';
	const obj = { foo: 'bar' };
	console.log(obj.foo); // => bar
	obj.foo = 'baz';
	console.log(obj.foo); // => baz
### 3.3 字符串扩展的一些新特性和API
#### 3.3.1 模板字符串
只要以后涉及到字符串拼接的业务，就直接使用模板字符串    `${a}${b}aaa`
先来看看以前是我们是拼接字符串的：

	var str = '<h1 id="'+id+'">
					<a href="'+href+'" class="headerlink" title="'+title+'">'+title+'</a>
			  </h1>';

对面上面那种方式及其容易出错，而且代码不够直观优雅，所以 es2015 中新增了一个全新的增强版字符串：模板字符串

	var str = `<h1 id="${id}">
	            <a href="${href}" class="headerlink" title="${title}">${title}</a>
	           </h1>`;

有了模板字符串，我们以后在拼接遇到拼接字符串的场景的时候就不用像以前那样写一大堆看不清楚的拼接了

模板字符串注意事项：
- 模板字符串使用反引号 ` `作为标识，在键盘左上角的Esc 下面（切换到英文状态才可以）
- 模板字符串中所有的空格和缩进都会被保留
- 在模板字符串中嵌入变量：${变量名}，可以使用多次

#### 3.3.2 字符串扩展的一些API

- includes(str)   表示是否找到了参数字符串
- startsWith(str) 表示参数字符串是否在源字符串的头部
- endsWith(str) 表示参数字符串是否在源字符串的尾部
- repeat(num) 将原字符串重复n次并返回


### 3.4 箭头函数

箭头函数就是一种简洁的函数语法糖而已，一般我们在需要使用一个匿名函数的时候，
就可以使用箭头函数来代替了，可以使我们的代码变得更优雅


使用箭头函数注意事项：

- 箭头函数一般用于一次性的函数，也就是匿名函数
- 箭头函数创建的函数不能被实例化
- 箭头函数内部没有 arguments 对象
## 4. 文件操作
### 4.1 Buffer
计算机最早诞生的时候，没有中文，在美国
26个英文字母，@ ! , . - + =
计算机只能识别 0 或者 1
把你的字符和计算机真正存储的二进制数据做了一个字典：
可以通过 开源中国 官网网站提供的一个工具页面：http://tool.oschina.net/
随着计算机普及到了世界各地，ASC II 码 已经不能满足世界各地人们的需求了
计算机进入中国之后，后来在原来的 ASC II 码基础之上扩展了一个新的字符集编码：gb2012，
用来支持中文
#### 4.1.1 创建Buffer

Buffer 是一个像 Array 的对象，它的元素为16进制的两位数（0-255的值），主要用于操作字节，
Buffer 是一个全局对象，使用的时候不需要 require

- new Buffer(size)
- new Buffer(str[,encoding])

#### 4.1.2 Buffer的一些属性

- buf[index] 通过下标访问 buffer 的某个字节的数据
- buf.indexOf(value[, byteOffset][, encoding]) 查找某个字符在 buffer 内存中的字节下标
- buf.includes(value[, byteOffset][, encoding])
- buf.length
- buf.slice([start[, end]])
- buf.toString([encoding[, start[, end]]])
- buf.write(string[, offset[, length]][, encoding])

#### 4.1.3 Buffer 的一些类方法

- Buffer.byteLength(string[, encoding])
- Buffer.concat(list[, totalLength])
- Buffer.isBuffer(obj)
- Buffer.isEncoding(encoding)

#### 4.1.4 造成乱码的原因

我们通常所说的编码一般就是指 字符集编码，一般用于字符串

当你把一个 `gbk` 编码文件发送给了你的一个国外友人的时候，
乱码的原因就是：他的机器上没有该编码　

计算机为了让多语言操作系统下可以识别和共享一种编码格式：所以诞生了 超级大字典：`utf-8`

造成乱码的原因其实就是　读取的编码和文件的编码不一致　

要想解决乱码：让文件编码和读取编码统一即可

- 什么是字符集编码
- 为什么要有编码
  + 计算机只能识别二进制
  + 为了让计算机可以识别字符，人类做了一个字典 二进制 -> 字符 的映射关系
- 为什么会产生乱码
  + 文件编码和读取该文件的编码不一致导致的
- 如何解决乱码
  + 让文件和读取的字符编码集一致即可
- 如何解决 Node 原生不支持的一些编码
  + 通过 第三方包：[iconv-lite ](https://www.npmjs.com/package/iconv-lite)
  + 该第三方包可以解决 gbk 等编码不支持的问题


#### 4.1.5 iconv-lite 基本使用

原生node对于某些编码并不支持，为了解决这个问题，
我们可以使用社区提供的一个包：`iconv-lite` 来解决node无法识别的编码的问题

首先，要下载 `iconv-lite` 到当前项目中

```
npm install iconv-lite --save
```

安装之后，就可以在项目中使用了

基本使用：
```javascript
// 引包
const iconv = require('iconv-lite');
 
// 将一个buffer对象按照 gbk 编码来解析，得到的就是一个 解码过后的 字符串
// 注意：前提是你要知道你的 buffer 对象中实际存储的是哪个编码生成的二进制数据
str = iconv.decode(new Buffer([0x68, 0x65, 0x6c, 0x6c, 0x6f]), 'gbk');
 
// 对字符串进行 gbk 编码，得到的就是一个进行 gbk 编码过后的二进制数据
buf = iconv.encode("Sample input string", 'gbk');

// 检查 iconv-lite 是否支持该编码
iconv.encodingExists("us-ascii")
```

## 5. 晚上补课

### 5.1 翻墙

![life without walls](life.jpeg)

#### VPN

![一图看懂vpn](vpn.gif)

#### vps

![一图看懂vps](vps.jpg)

#### shadowsocks

[直接购买](http://www.shadowsocks.com)

[免费 shadowsocks 账号](http://www.ishadowsocks.net/)

[一个比较实惠的vps](https://bandwagonhost.com/)

[自己搭建翻墙服务器](http://shadowsocks.blogspot.com/)

[蓝灯](https://getlantern.org/)

### 5.2 利用 github 免费空间部署自己的个人网站

1. 注册 github 账号
2. 登陆自己的 github 账号
3. 在右上角 找到一个 +号的坐标：选择 New repository 表示新建一个仓库
4. 仓库的名字就用：`你的用户名.github.io` 如果不使用自己的用户名无效
5. 填写完 仓库名称之后，选择下面的 `Create repository` 创建该仓库
6. 创建完成之后自动跳转到了一个页面，然后选择切换到 `HTTPS` 
7. 将后面的仓库地址复制出来
8. 回到操作系统中，找到一个目录
9. 在该目录下 执行： `git clone https://github.com/iroc/iroc.github.io.git`
10. 通过 Sublime 打开该目录，在该目录下新建一个文件 `index.html`
11. 在该文件中写自己的页面就可以了
12. 编辑完之后，在命令行中输入：`git add .`
13. 然后 `git commit -m "2016-5-3 20:17:48"`
14. 然后 `git push`
15. 执行完 `git push` 之后，需要输入自己的github用户名和密码，然后才能提交到github上
16. 最后就可以通过 `iroc.github.io`

### 5.3 修改注册表在鼠标右键中加入  `Open With Sublime Text` 选项

1. 打开注册表编辑器，win+r 输入 regdit
2. 查找该节点
HKEY_CLASSSES_ROOT→ * → Shell 
3. 在该节点下新建项名为 Open With Sublime Text 3
4. 在右边窗口新建字符串值  右键--新建--字符串值，名称为Icon，值：C:\Program\Sublime Text 3\sublime_text.exe,0
5. 在新建的项下面新建项 command。修改右侧窗口中的默认值，修改为：C:\Program Files\Sublime Text 3\sublime_text.exe "%1"
退出，测试是否生效

### YouTube最火短片：[盖章](https://www.youtube.com/watch?v=mLlAWzvoCRU)

- smile
- great
- awesome
- amazing
