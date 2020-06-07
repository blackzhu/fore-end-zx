# HTTP
[建议精读）HTTP灵魂之问，巩固你的 HTTP 知识体系](https://juejin.im/post/5e76bd516fb9a07cce750746)

### 001. HTTP 报文结构是怎样的？
起始行 + 头部 + 空行 + 实体
### 002. 如何理解 HTTP 的请求方法？
#### GET 和 POST 有什么区别？
* GET在浏览器回退时是无害的，而POST会再次请求；  
* 从缓存的角度，GET 请求会被浏览器主动缓存下来，留下历史记录，而 POST 默认不会。  
* GET请求会被浏览器互动缓存，而POST不会，除非手动设置；  
* GET请求参数会被完整的保留在浏览器历史记录中，而POST不会；  
* GET参数通过url传递长度有限制，POST没有；  
* 从参数的角度，GET 一般放在 URL 中，因此不安全，POST 放在请求体中，更适合传输敏感信息。  
* 从TCP的角度，GET 请求会把请求报文一次性发出去，而 POST 会分为两个 TCP 数据包，首先发 header 部分，如果服务器响应 100(continue)， 
然后发 body 部分。(火狐浏览器除外，它的 POST 请求只发一个 TCP 包)
### 003: 如何理解 URI？
### 004: 如何理解 HTTP 状态码？
RFC 规定 HTTP 的状态码为三位数，被分为五类:
* 1xx: 表示目前是协议处理的中间状态，还需要后续操作。
* 2xx: 表示成功状态。
* 3xx: 重定向状态，资源位置发生变动，需要重新请求。
* 4xx: 请求报文有误。
* 5xx: 服务器端发生错误。
### 005: 简要概括一下 HTTP 的特点？HTTP 有哪些缺点？
* 无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
* 无状态：无状态是指协议对于事务处理没有记忆能力，服务器不知道客户端是什么状态。即我们给服务器发送 HTTP 请求之后，服务器根据请求，
会给我们发送数据过来，但是，发送完，不会记录任何信息。
* 简单快速：请求-应答。也就是一发一收、有来有回
* 灵活可扩展：主要体现在两个方面。一个是语义上的自由，只规定了基本格式，比如空格分隔单词，换行分隔字段，其他的各个部分都没有严格的语法限制。
另一个是传输形式的多样性，不仅仅可以传输文本，还能传输图片、视频等任意数据，非常方便。
####  缺点
明文传输；队头阻塞问题；或许是无状态
### 006: 对 Accept 系列字段了解多少？
数据格式、压缩方式、支持语言和字符集。
### 007: 对于定长和不定长的数据，HTTP 是怎么传输的？
### 008: HTTP 如何处理大文件的传输？
### 009: HTTP 中如何处理表单数据的提交？
### 010: HTTP1.1 如何解决 HTTP 的队头阻塞问题？
### 011: 对 Cookie 了解多少？
### 012: 如何理解 HTTP 代理？
### 013: 如何理解 HTTP 缓存及缓存代理？
### 014: 什么是跨域？浏览器如何拦截响应？如何解决？
[cros实现跨域请求](https://blog.csdn.net/badmoonc/article/details/82706246)

#### JSONP
动态创建<script>标签，设置其src，回调函数在src中设置：  
var script = document.createElement("script");  
script.src = "https://api.douban.com/v2/book/search?q=javascript&count=1&callback=handleResponse";  
document.body.insertBefore(script, document.body.firstChild);  
<script type="text/javascript"> function handleResponse(response){ console.log(response); } </script>  

#### Hash 
hash是url中#后面的，search是url中？后面的，其中hash不会刷新页面，search会。  
当前页面A通过Iframe嵌入了跨域页面B  
A中代码：  
var B = document.getElementByTagName('iframe');  
B.src = B.src + "#" + 'data';  
在B页面中：  
window.onhashChange = function () {  
  var data = window.location.hash;  
}  
#### postMessage
A页面中代码：  
window.postMessage('data',http://www.b.com);  
B中代码：  
window.addEventListener('message',function(e){  
  console.log(e.data);  
})  
#### webSocket 
let socket = new WebSocket("ws://localhost:3000");//ws协议是webSocket自己创造的   
socket.onopen = function(){ socket.send("connection open"); }   
socket.onmessage = function(e){ console.log('receive msg',e.data); socket.close() }   

### 015: TLS1.2 握手的过程是怎样的？

### 016: TLS 1.3 做了哪些改进？
