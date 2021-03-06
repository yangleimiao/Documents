HTTP

---

##### 请求方式有几种？

**HEAD** 获取响应消息头，并且这些头部与HTTP GET 方法请求时返回的一致

**GET** 向特定的资源发出请求

**POST** 向指定资源提交数据进行处理请求

> 上面3个是1.0中定义的，下面5个是1.1新增

**PUT** 向指定资源位置上传最新内容

**DELETE** 请求服务器删除Request-URL所标识的资源

**TRACE** 回显服务器收到的请求，主要用于测试或诊断

**CONNECT** HTTP1.1中预留给能够将连接改为管道方式的代理服务器

**OPTIONS** 返回服务器针对特定资源所支持的HTTP请求方法



##### PUT和POST的区别

PUT方法是幂等的，连续调用一次或多次的效果相同，POST是非幂等的；

PUT的URL指向单一资源，POST可以指向资源集合



##### GET与POST有什么区别？

GET是请求获得数据，POST是提交数据；

GET是安全且幂等的，POST是非安全和非幂等的；

GET通过URL传输数据，POST的数据通过请求体传输；

> 安全：只读，使用这个方法不会引起服务器状态变化；
>
> 幂等：同一个请求方法执行多次和执行一次的效果相同



##### 常用状态码

2XX 成功

* 200 OK，表示从客户端发来的请求在服务端被正确处理
* 204 No Content，表示请求成功，但响应报文不含实体的主体部分
* 206 Partial Content，进行范围请求

3XX 重定向

* 301 moved permanently，永久性重定向，表示资源已被分配了新的URL
* 302 found，临时性重定向，表示资源临时被分配了新的URL
* 303 see other，表示资源存在另一个URL
* 304 not modified，
* 307 temporary redirect，临时重定向

4XX 客户端错误

* 400 bad request，请求报文存在语法错误
* 401 unauthorized，表示发送的请求需要有同感HTTP认证的认证信息
* 403 forbidden，表示对请求资源的访问被服务器拒绝
* 404 not found，表示在服务器上没有找到请求的资源

5XX 客户端错误

* 500 internal sever error，表示服务器端在执行请求时发生了错误
* 503 service unavailable，表示服务器暂时处于超负载或正在停机维护，无法处理请求



307、303、302状态码的区别？

302是HTTP1.0的状态码，在1.1版本细化出303和307；

303明确表示客户端应当采用get方法获取资源，会把POST变为GET进行重定向，307不会从POST变为GET；



##### HTTP协议格式

请求和响应的消息协议是一样的，分为三个部分，起始行、消息头和消息体，三个部分以CRLF为分隔符；

HTTP请求的起始行称为请求行；响应的起始行为状态行；

消息头部由很多键值对组成，多个键值对直接用CRLF作为分隔符，



##### HTTP的无状态性

HTTP协议的无状态性是指服务器的协议层无需为不同的请求之间建立任何相关关系；

这不代表建立在HTTP协议之上的应用程序就无法维持状态，应用层可以通过会话Session来跟踪用户请求之间的相关性，服务器会为每个会话对象绑定一个唯一的会话ID，浏览器可以将会话ID记录在本地缓存LocalStorage或者Cookie，在后续的请求都带上这个会话ID，服务器就可以为每个请求找到相应的会话状态。



#####  输入url到页面加载都发生了什么？

- 输入地址
- 浏览器查找域名的 IP 地址这一步包括 DNS 具体的查找过程，包括：浏览器缓存->系统缓存->路由器缓存…
- 浏览器向 web 服务器发送一个 HTTP 请求
- 服务器的永久重定向响应（从 http://example.com 到 http://www.example.com）
- 浏览器跟踪重定向地址
- 服务器处理请求
- 服务器返回一个 HTTP 响应
- 浏览器显示 HTML
- 浏览器发送请求获取嵌入在 HTML 中的资源（如图片、音频、视频、CSS、JS等等）
- 浏览器发送异步请求





HTTP2相对于HTTP1.X有什么优势和特点

**二进制分帧**

http2采用二进制格式传输数据，而非Http1.x的文本格式

**服务器推送**

* 服务端可以在发送页面HTML时主动推送其他资源，而不用等到浏览器解析到相应位置发起请求再响应；

**头部压缩**

* HTTP1.X会在请求和响应中重复携带不常改变的、冗长的头部数据；HTTP2在客户端和服务端使用“首部表”来跟踪和存储之前发生的键值对，对于相同的数据，不再通过每次请求和响应发送；

* 首部表在HTTP2的连接存续期内始终存在，有客户端和服务端共同更新；





##### 一次完整的HTTP请求需要经历哪些步骤？

* 建立TCP连接

* Web浏览器向Web服务器发送请求行

  建立TCP连接后，Web浏览器会向Web服务器发送请求命令；

* Web浏览器发送请求头

* Web服务器应答

  客户机向服务器发出请求后，服务器向客户回送应答；

* Web服务器发送应答头

* Web服务器向浏览器发送数据

  发送应答头后，以Content-Type应答头信息描述的格式发送请求的实际数据；

* Web服务器关闭TCP连接

  

#####  HTTPS与HTTP有什么区别？

HTTP是明文传输，未加安全加密的协议，有安全上的风险；

HTTPS加了SSL/TLS协议，是安全的协议；

HTTP默认端口是80，HTTPS默认端口443；



##### HTTPS工作原理

首先HTTP请求服务端生成证书，客户端对证书的有效性，合法性、域名是否与请求的域名一致、证书的公钥（RSA加密）等进行校验；

客户端如果校验通过后，就根据证书的公钥的有效， 生成随机数，随机数使用公钥进行加密（RSA加密）；

消息体产生的后，对它的摘要进行MD5（或者SHA1）算法加密，此时就得到了RSA签名；

发送给服务端，此时只有服务端（RSA私钥）能解密。

解密得到的随机数，再用AES加密，作为密钥（此时的密钥只有客户端和服务端知道）



##### HTTPS如何保证安全的？

* 结合对称加密和非对称加密，将对称加密的密钥使用非对称加密的公钥进行加密，然后发送出去，接收方使用私钥进行解密得到对称加密的密钥，然后双方使用对称加密进行沟通；

* 解决中间人问题：需要第三方颁发的证书（CA），防止中间人攻击

  > 中间人攻击：如果客户端和服务端之间存在一个中间人，这个中间人只需把原本双方通信互发的公钥换成自己的公钥，这样中间人就可以轻松解密通信双方所发送的所有数据；

  正式包括：签发者，证书用途、使用者公钥、使用者私钥、使用者的HASH算法，证书到期时间等；

  为了防止中间人篡改证书，需要数字签名技术，用CA自带的HASH算法对证书内容进行HASH得到一个摘要，再用CA的私钥加密，最终组成数字签名；当别人把他的证书发过来的时候，再用同样的HASH算法，生成消息摘要，然后用CA的公钥对数字签名解密，得到CA创建的消息摘要，两者 一比就知道有没有被篡改了；

































