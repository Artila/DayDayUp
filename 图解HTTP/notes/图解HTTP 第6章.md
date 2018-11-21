## 图解HTTP 第6章

—— HTTP 首部

> HTTP 协议的请求和响应报文中必定包含HTTP首部，只是我们平时在使用 Web的过程中感受不到它。本章学习HTTP首部的结构，以及首部中各字段的用法。



1. HTTP 报文首部：

   ![HTTP报文的结构.jpg](https://upload-images.jianshu.io/upload_images/1331173-30e37573b1bb4bef.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   HTTP 协议的请求和响应报文中必定包含HTTP首部。

   首部内容为客户端和服务器分别处理请求和响应提供所需要的信息。

   对于客户端用户来说，这些信息中的大部分内容都无须亲自查看。

   报文首部由几个字段构成。

   - HTTP 请求报文：在请求中，HTTP 报文由方法、URI、HTTP版本、HTTP 首部字段等部分构成。

     ![请求报文.jpg](https://upload-images.jianshu.io/upload_images/1331173-f3358131073396ed.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - HTTP 响应报文：在响应中，HTTP 报文由 HTTP 版本、状态码（数字和原因短语）、HTTP 首部字段3部分构成。

2. 