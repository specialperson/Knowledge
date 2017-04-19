# Knowledge

## UDP,HTTP

* [UDP/Datagram](https://github.com/ElemeFE/node-interview/blob/master/sections/network.md#udp)
* [HTTP](https://github.com/ElemeFE/node-interview/blob/master/sections/network.md#http)

## UDP

* TCP/UDP 的区别? UDP 有粘包吗?

| 协议   | 连接性                       | 双工性      | 可靠性          | 有序性         | 有界性                                      | 拥塞控制 | 传输速度 | 量级   | 头部大小    |
| ---- | ------------------------- | -------- | ------------ | ----------- | ---------------------------------------- | ---- | ---- | ---- | ------- |
| TCP  | 面向连接(Connection oriented) | 全双工(1:1) | 可靠(重传机制)     | 有序(通过SYN排序) | 无, 有[粘包情况](https://github.com/ElemeFE/node-interview/blob/master/sections/network.md#%E7%B2%98%E5%8C%85) | 有    | 慢    | 低    | 20~60字节 |
| UDP  | 无连接(Connection less)      | n:m      | 不可靠(丢包后数据丢失) | 无序          | 有消息边界, **无粘包**                           | 无    | 快    | 高    | 8字节     |

UDP socket 支持 n 对 m的连接状态

### 常见的应用场景

| 传输层协议 | 应用      | 应用层协议  |
| ----- | ------- | ------ |
| TCP   | 电子邮件    | SMTP   |
|       | 终端连接    | TELNET |
|       | 终端连接    | SSH    |
|       | 万维网     | HTTP   |
|       | 文件传输    | FTP    |
| UDP   | 域名解析    | DNS    |
|       | 简单文件传输  | TFTP   |
|       | 网络时间校对  | NTP    |
|       | 网络文件系统  | NFS    |
|       | 路由选择    | RIP    |
|       | IP电话    | -      |
|       | 流式多媒体通信 | -      |

***从表中可以得到, UDP 速度快, 开销低, 不用封包/拆包允许丢一部分数据, 监控统计/日志数据上报/流媒体通信等场景都可以用 UDP. 目前 Node.js 的项目中使用 UDP 比较流行的是 [StatsD](https://github.com/etsy/statsd) 监控服务.

### HTTP

[超文本传输协议](http://baike.baidu.com/item/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)（HTTP，HyperText Transfer Protocol)是[互联网](http://baike.baidu.com/item/%E4%BA%92%E8%81%94%E7%BD%91)上应用最为广泛的一种[网络协议](http://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E5%8D%8F%E8%AE%AE)。所有的[WWW](http://baike.baidu.com/item/WWW)文件都必须遵守这个标准。设计HTTP最初的目的是为了提供一种发布和接收[HTML](http://baike.baidu.com/item/HTML)页面的方法。

#### 技术架构

HTTP是一个[客户端](http://baike.baidu.com/item/%E5%AE%A2%E6%88%B7%E7%AB%AF)和[服务器](http://baike.baidu.com/item/%E6%9C%8D%E5%8A%A1%E5%99%A8)端请求和应答的标准（TCP）。客户端是终端用户，服务器端是网站。通过使用[Web浏览器](http://baike.baidu.com/item/Web%E6%B5%8F%E8%A7%88%E5%99%A8)、[网络爬虫](http://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB)或者其它的工具，客户端发起一个到服务器上指定端口（默认[端口](http://baike.baidu.com/item/%E7%AB%AF%E5%8F%A3)为80）的HTTP请求。（我们称这个客户端）叫用户代理（user agent）。

事实上，HTTP可以在任何其他互联网协议上，或者在其他网络上实现。HTTP只假定（其下层协议提供）可靠的传输，任何能够提供这种保证的协议都可以被其使用。

通常，由HTTP客户端发起一个请求，建立一个到服务器指定端口（默认是[80端口](http://baike.baidu.com/item/80%E7%AB%AF%E5%8F%A3)）的TCP连接。HTTP服务器则在那个端口监听客户端发送过来的请求。一旦收到请求，服务器（向客户端）发回一个状态行,HTTP使用TCP而不是UDP的原因在于（打开）一个网页必须传送很多数据，而TCP协议提供传输控制，按顺序组织数据，和错误纠正。

### 协议功能

HTTP协议是用于从WWW服务器传输超文本到本地浏览器的传输协议。它可以使浏览器更加高效，使网络传输减少。它不仅保证计算机正确快速地传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示(如文本先于图形)等。

HTTP是客户端浏览器或其他程序与[Web服务](http://baike.baidu.com/item/Web%E6%9C%8D%E5%8A%A1)器之间的应用层通信协议。

我们在浏览器的地址栏里输入的网站地址叫做URL.当你在浏览器的地址栏中输入一个URL或是单机一个超链接时,URL就确定了要浏览的地址.。浏览器通过超文本传输协议(HTTP)，将Web服务器上站点的网页代码提取出来，并翻译成网页.

### 运作方式

在WWW中，“客户”与“服务器”是一个相对的概念，只存在于一个特定的连接期间，即在某个连接中的客户在另一个连接中可能作为服务器。基于HTTP协议的客户/服务器模式的信息交换过程，它分四个过程：建立连接、发送请求信息、发送响应信息、关闭连接。

HTTP协议是基于请求/响应[范式](http://baike.baidu.com/item/%E8%8C%83%E5%BC%8F)的。

#### method/status

```
const http = require('http');
console.log(http.METHODS);
console.log(http.STATUS_CODES);
```

**通过打印上面代码可以得到http的方法和状态(状态码对应的意思是什么)

>GET 和 POST 的区别

主要分为以下三点:

(1) GET使用URL拼接参数或Cookie传递参数.而POST则是将数据放在body中.

(2) GET的URL长度有限制,因此传递数据有限,而POST的数据可以非常大

(3) POST相对安全.因为GET请求地址栏可以看到数据

#### headers

HTTP headers 是在进行 HTTP 请求的交互过程中互相支会对方一些信息的主要字段.

>cookie 与 session 的区别,服务端如何清除 cookie

主要区别在于, session 存在服务端, cookie 存在客户端. session 比 cookie 更安全. 而且 cookie 不一定一直能用 (可能被浏览器关掉). 服务端可以通过设置 cookie 的值为空并设置一个及时的 expires 来清除存在客户端上的 cookie.

>什么是跨域请求, 如何允许跨域

向不同域名的请求被称作跨域请求 . 默认情况下使用 XMLHttpRequest 和 Fetch 发起 HTTP 请求必须遵守同源策略, 即只能向相同域名请求.

### Agent

Node.js 中的 `http.Agent` 用于池化 HTTP 客户端请求的 socket. 也就是复用 HTTP 请求时候的 socket. 如果你没有指定 Agent 的话, 默认用的是 `http.globalAgent`.

### socket hang up

hang up 有挂断的意思, socket hang up 也可以理解为 socket 被挂断. 在 Node.js 中当你要 response 一个请求的时候, 发现该这个 socket 已经被 "挂断", 就会就会报 socket hang up 错误.