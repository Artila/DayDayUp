### 图解HTTP 第二章

——简单的HTTP协议

本章将针对HTTP协议结构进行讲解，主要使用HTTP/1.1版本。



1. HTTP协议和TCP/IP协议族内的其他众多的协议相同，用于客户端和服务器之间的通信。

2. 请求访问文本或图像等资源的一端称为客户端，而提供资源响应的一端称为服务器端。

3. 应用HTTP协议时，必定是一端担任客户端角色，另一端担任服务器端角色。

4. HTTP协议规定，请求从客户端发出，最后服务器端响应该请求并返回。换句话说，肯定是先从客户端开始建立通信的，服务器端在没有接收到请求之前不会发送响应。

   ![HTTP协议的请求和响应.jpg](https://upload-images.jianshu.io/upload_images/1331173-d3927eef51d1e9d9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 下面则是从客户端发送给某个HTTP服务器端的请求报文中的内容。

   ```
   GET /index.htm HTTP/1.1
   Host: hackr.jp
   ```

   - `GET`：表示请求访问服务器的类型，称为方法（method）。

   - `/index.htm`：指明了请求访问的资源对象，也叫请求URI（request-URI）

   - `HTTP/1.1`：HTTP的版本号，用来提示客户端使用的HTTP协议功能

     综合来看，这段请求内容的意思是：请求访问某台HTTP服务器上的/index.htm页面资源。

     请求报文是由请求方法、请求URI、协议版本、可选的请求首部字段和内容实体构成的。

     ![请求报文的构成.jpg](https://upload-images.jianshu.io/upload_images/1331173-3e6cbe2a7e8f9332.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 接收到请求的服务器，会将请求内容的处理结果以响应的形式返回。

   ```
   HTTP/1.1 200 OK
   Date: Tue, 10 Jul 2012 06:50:15 GMT
   Content-length: 362
   Content-Type: text/html
   
   <html>
   ……
   ```

   - `HTTP/1.1`：表示服务器对应的HTTP版本

   - `200 OK`：表示请求的处理结果的状态码（status code）和原因短语（reason-phrase）。

   - `Date`：创建响应的日期时间，是首部字段（header field）内的一个属性。

   - 一空行：分隔，之后的内容称为资源实体的主体（entity body）。

     响应报文基本上由协议版本、状态码（表示请求成功或失败的数字代码）、用以解释状态码的原因短语、可选的响应首部字段以及实体主体构成。

     ![响应报文的构成.jpg](https://upload-images.jianshu.io/upload_images/1331173-2e2fdc18974907d6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7. HTTP是一种不保存状态，即无状态（stateless）协议。HTTP协议自身不对请求和响应之间的通信状态进行保存。也就是说在HTTP这个级别，协议对于发送过的请求或响应都不做持久化处理。

8. 使用HTTP协议，每当有新的请求发送时，就会有对应的新响应产生。协议本身并不保留之前一切的请求或响应报文的信息。这是为了更快地处理大量事务，确保协议地可伸缩性，而特意把HTTP协议设计成如此简单地。

9. HTTP/1.1 虽然是无状态协议，但为了实现期望地保持状态功能，于是引入了Cookie技术。有了Cookie再用HTTP协议通信，就可以管理状态了。

10. 如果不是访问特定资源而是对服务器本身发起请求，可以用一个*来代替请求URI。下面这个例子是查询HTTP服务器端支持的HTTP方法种类。

   ```
   OPTIONS * HTTP/1.1
   ```

11. HTTP协议的初始版本中，每进行一次HTTP通信就要断开一次TCP连接。

    ![断开TCP连接.jpg](https://upload-images.jianshu.io/upload_images/1331173-a1908810dcf1e95f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    以当年的通信情况来说，因为都是些容量很小的文本传输，所以即使这样也没有多大问题。可随着HTTP的普及，文档中包含大量图片的情况多了起来。

    比如，使用浏览器浏览一个包含多张图片的HTML页面时，在发送请求访问HTML页面资源的同时，也会请求该HTML页面里包含的资源。因此，每次的请求都会造成无谓的TCP连接建立和断开，增加通信量的开销。

12. 为解决上述TCP连接的问题，HTTP/1.1 和一部分的 HTTP/1.0 , 想出了持久连接（HTTP Persistent Connections，也称为 HTTP keep-alive 或 HTTP connection reuse）的方法。持久连接的特点是，只要任意一端没有明确提出断开连接，则保持TCP连接状态。

13. 持久连接旨在建立1次TCP连接后进行多次请求和响应的交互。

14. 持久连接的好处在于减少了TCP连接的重复建立和断开所造成的额外开销，减轻了服务器端的负载。另外，减少开销的那部分时间，使HTTP请求和响应能够更早地结束，这样Web页面地显示速度也就相应提高了。

15. 在HTTP/1.1中，所有的连接默认都是持久连接，但在HTTP/1.0内并未标准化。虽然有一部分服务器通过非标准的手段实现了持久连接，但服务器端不一定能够支持持久连接。毫无疑问，除了服务器端，客户端也需要支持持久连接。

16. 持久连接使得多数请求以管线化（pipelining）方式发送称为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不用等待响应亦可直接发送下一个请求。

    这样就能够做到同时并行发送多个请求，而不需要一个接一个地等待响应了。

    比如，当请求一个包含10张图片的 HTML Web 页面，与挨个连接相比，用持久连接可以让请求更快结束。而管线化技术则比持久连接还要快。请求数越多，时间差就越明显。

17. 无状态协议当然也有它的优点。由于不必保存状态，自然可减少服务器的 CPU 及内存资源的消耗。从另一侧面来说，也正是因为 HTTP 协议本身是非常简单的，所以才会被应用在各种场景里。

18. Cookie 技术通过在请求和响应报文中写入Cookie信息来控制客户端的状态。

    Cookie 会根据从服务器端发送的响应报文内的一个叫做 Set-Cookie 的首部字段信息，通知客户端保存 Cookie。当下次客户端再往服务器发送请求时，客户端会自动在请求报文中加入 Cookie 值后发送出去。

    服务器端发现客户端发送过来的 Cookie 后，会去检查究竟时从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后得到之前的状态信息。

    ![Cookie.jpg](https://upload-images.jianshu.io/upload_images/1331173-8069b429ca9bf5ec.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    上图展示了发生 Cookie 交互的情景，HTTP 请求报文和响应报文的内容如下。

    1. 请求报文（没有 Cookie 信息的状态）

       ```
       GET /reader/ HTTP/1.1
       Host: hackr.jp
       * 首部字段内没有 Cookie 的相关信息
       ```

    2. 响应报文（服务器端生成 Cookie 信息）

       ```
       HTTP/1.1 200 OK
       Date: Thu, 12 Jul 2012 07:12:20 GMT
       Server: Apache
       <Set-Cookie: sid=1342077140226724; path=/; expires=Wed, => 10-Oct-12 07:12:20 GMT>
       Content-Type: text/plain; charset=UTF-8
       ```

    3. 请求报文（自动发送保存着的 Cookie 信息）

       ```
       GET /image/ HTTP/1.1
       Host: hackr.jp
       Cookie：sid=1342077140226724
       ```

19. 































