### 图解HTTP 第3章

——HTTP 报文内的 HTTP 信息

> HTTP通信过程包括从客户端发往服务器端的请求及从服务器端返回客户端的响应。本章了解一下请求和响应是怎样运作的。



1. 用于 HTTP 协议交互的信息被称为HTTP报文。

2. 请求端（客户端）的HTTP报文叫做请求报文，响应端（服务器端）的叫做响应报文。

3. HTTP 报文本身是由多行（用 CR+LF 作换行符）数据构成的字符串文本。

4. HTTP 报文大致可分为报文首部和报文主体两块。两者由最初出行的空行（ CR+LF ）来划分。通常，并不一定要有报文主体。

   ![HTTP报文的构成.jpg](https://upload-images.jianshu.io/upload_images/1331173-50745b74e895b18d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 

























