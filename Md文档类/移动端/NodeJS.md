# Nodejs



## 介绍

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，是一个应用程序。

官方网址 <https://nodejs.org/en/>，中文站 <http://nodejs.cn/>



## 作用

- 解析运行 JS 代码
- 操作系统资源，如内存、硬盘、网络
- 创建 WEB 服务



## 使用

### 下载安装

工具一定要到官方下载，历史版本下载 <https://npm.taobao.org/mirrors/node/>

![img](https://ask.qcloudimg.com/http-save/5418473/ofyhyf210r.jpeg?imageView2/2/w/1620)

Nodejs 的版本号奇数为开发版本，偶数为发布版本，<span style="color:red">我们选择偶数号的 LTS 版本（长期维护版本 long term service）</span>

![1572676490692](assets/1572676490692.png)

双击打开安装文件，一路下一步即可😎，默认的安装路径是 `C:\Program Files\nodejs`

安装完成后，在 CMD 命令行窗口下运行 `node -v`，如显示版本号则证明安装成功，反之安装失败，重新安装。 

![1572678177784](assets/1572678177784.png)

### 初体验

#### 交互模式

在命令行下输入命令 `node`，这时进入 nodejs 的交互模式

![1572678681282](assets/1572678681282.png)

#### 文件执行

创建文件 hello.js ，并写入代码 console.log('hello world')，命令行运行 `node hello.js`

快速启动命令行的方法

* 在文件夹上方的路径中，直接输入 cmd 即可
* 在文件夹空白区域，右键+shift 可以看见一个菜单
* 使用 webstorm 和 vscode 自带的命令行窗口

![1572680753835](assets/1572680753835.png)

#### webstorm 下运行

webstorm 的 node 配置 ， ==files -> settings -> 搜索 node -> 右侧选取 node.exe== 的位置

![1572681362125](assets/1572681362125.png)

#### 注意

<span style="color:red">在 nodejs 环境下，不能使用 BOM 和 DOM ，也没有全局对象 window，全局对象的名字叫 global</span>



### Buffer

#### 介绍

Buffer 是一个和数组类似的对象，不同是 Buffer 是专门用来保存二进制数据的

#### 特点

* 大小固定：在创建时就确定了，且无法调整
* 性能较好：直接对计算机的内存进行操作
* 每个元素大小为 1 字节（byte）

#### 操作

##### 创建 Buffer

* 直接创建 Buffer.alloc
* 不安全创建 Buffer.allocUnsafe

* 通过数组和字符串创建 Buffer.from

##### Buffer 读取和写入

可以直接通过 `[]` 的方式对数据进行处理，可以使用 toString 方法将 Buffer 输出为字符串

##### 关于溢出

溢出的高位数据会舍弃

##### 关于中文

一个 UTF-8 的中文字符大多数情况都是占 3 个字节

##### 关于单位换算

1Bit 对应的是 1 个二进制位

8 Bit = 1 字节（Byte）

1024Byte = 1KB 

1024KB = 1MB

1024MB = 1GB

1024GB = 1TB

平时所说的网速 10M 20M 100M 这里指的是 Bit ，所以理论下载速度 除以 8 才是正常的理解的下载速度

### 文件系统 fs

fs 全称为 file system，是 NodeJS 中的内置模块，可以对计算机中的文件进行增删改查等操作。

##### 文件写入

* 简单写入
  * fs.writeFile(file, data, [,options], callback);
  * fs.writeFileSync(file, data);
  * options 选项
    * `encoding` **默认值:** `'utf8'`
    * `mode`**默认值:** `0o666`
    * `flag` **默认值:** `'w'`
* 流式写入
  * fs.createWriteStream(path[, options])
    * path
    * options
      * ==flags==   **默认值:** `'w'`
      * `encoding `**默认值:** `'utf8'`
      * `mode`   **默认值:** `0o666`
    * 事件监听 open  close  eg:  ws.on('open', function(){});

##### 文件读取

* 简单读取
  * fs.readFile(file, function(err, data){})
  * fs.readFileSync(file)
* 流式读取
  * fs.createReadStream();

##### 文件删除

* fs.unlink('./test.log', function(){});
* fs.unlinkSync('./move.txt');

##### 移动文件 + 重命名

* fs.rename('./1.log', '2.log', function(){})
* fs.renameSync('1.log','2.log')

##### 文件夹操作

* mkdir  创建文件夹
  * path
  * options 
    * recursive 是否递归调用
    * mode  权限 默认为 0o777
  * callback 
* rmdir 删除文件夹
* readdir  读取文件夹

### HTTP 协议



### WEB 服务

使用 nodejs 创建 HTTP 服务器

```js
//1. 引入 http 内置模块
var http = require('http');

//2. 创建服务
var server = http.createServer(function(request, response){
    response.end('hello world!!');
});

//3. 监听端口
server.listen(8000);
```

* request 是对请求报文的封装对象
* response 是对响应的封装对象

#### 获取请求

```js
//获取请求方法
console.log(request.method);

//获取http版本
console.log(request.httpVersion);

//获取请求路径
console.log(request.url);

//获取请求头
console.log(request.headers);

//获取请求体
request.on('data', function(chunk){})
request.on('end', function(){});
```

#### 设置响应

```js
//设置状态码
response.statusCode = 200;

//设置响应头
response.setHeader('content-type','text/html;charset-utf-8');

//设置响应体
response.write('body');

//结束
response.end();

```

#### 静态资源服务
