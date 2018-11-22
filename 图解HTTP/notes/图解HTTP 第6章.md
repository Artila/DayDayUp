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

     ![响应报文.jpg](https://upload-images.jianshu.io/upload_images/1331173-854a926c45df83b2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

   - 在报文众多的字段当中，HTTP首部字段包含的信息最为丰富。首部字段同时存在于请求和响应报文内，并涵盖HTTP报文相关的内容信息。

2. 使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等内容。

3. HTTP首部字段是由首部字段名和字段值构成的，中间用冒号“：”分隔。

4. **HTTP首部字段重复了会如何**：当HTTP报文首部中出现了两个或两个以上具有相同首部字段名时会怎么样？这种情况在规范内尚未明确，根据浏览器内部处理逻辑的不同，结果可能并不一致。有些浏览器会优先处理第一次出现的首部字段，而有些则会优先处理最后出现的首部字段。

5. **HTTP首部字段类型**：

   - 通用首部字段（General Header Fields）：请求报文和响应报文两方都会使用的首部
   - 请求首部字段（Request Header Fields）：请求报文使用的首部，补充了请求的附加内容、客户端信息、响应内容相关优先级等信息
   - 响应首部字段（Response Header Fields）：响应报文使用的首部，补充了响应的附加内容，也会要求客户端附加额外的内容信息
   - 实体首部字段（Entity Header Fields）：请求报文和响应报文的实体部分使用的首部。补充了资源内容更新时间等与实体有关的信息

6. HTTP/1.1 规范定义了47种首部字段。

7. 通用首部字段：

   | 首部字段名        | 说明                                                |
   | ----------------- | --------------------------------------------------- |
   | Cache-Control     | 控制缓存的行为                                      |
   | Connection        | 逐段首部、连接的管理                                |
   | Date              | 创建报文的日期时间                                  |
   | Pragma            | 在HTTP/1.0规定，与Cache-Control: no-cache效果一致。 |
   | Trailer           | 报文末端的首部一览                                  |
   | Transfer-Encoding | 指定报文主体的传输编码格式                          |
   | Upgrade           | 升级为其他协议                                      |
   | Via               | 代理服务器的相关信息                                |
   | Warning           | 错误通知                                            |

8. 请求首部字段：

   | 首部字段名          | 说明                                          |
   | ------------------- | --------------------------------------------- |
   | Accept              | 用户代理可处理的媒体类型                      |
   | Accept-Charset      | 优先的字符集                                  |
   | Accept-Encoding     | 优先的内容编码                                |
   | Accept-Language     | 优先的语言（自然语言）                        |
   | Authorization       | Web认证信息                                   |
   | Expect              | 期待服务器的特定行为                          |
   | From                | 用户的电子邮箱地址                            |
   | Host                | 请求资源所在服务器                            |
   | If-Match            | 比较实体标记（ETag）                          |
   | If-Modified-Since   | 比较资源的更新时间                            |
   | If-None-Match       | 比较实体标记（与If-Match相反）                |
   | If-Range            | 资源未更新时发送实体Byte的范围请求            |
   | If-Unmodified-Since | 比较资源的更新时间（与If-Modified-Since相反） |
   | Max-Forwards        | 最大传输逐跳数                                |
   | Proxy-Authorization | 代理服务器要求客户端的认证信息                |
   | Range               | 实体的字节范围请求                            |
   | Referer             | 对请求中的URI的原始获取方                     |
   | TE                  | 传输编码的优先级                              |
   | User-Agent          | HTTP客户端程序的信息                          |

9. 响应首部字段

   | 首部字段名         | 说明                         |
   | ------------------ | ---------------------------- |
   | Accept-Ranges      | 是否接受字节范围请求         |
   | Age                | 推算资源创建经过时间         |
   | ETag               | 资源的匹配信息               |
   | Location           | 令客户端重定向至指定URI      |
   | Proxy-Authenticate | 代理服务器对客户端的认证信息 |
   | Retry-After        | 对再次发起请求的时机要求     |
   | Server             | HTTP 服务器的安装信息        |
   | Vary               | 代理服务器缓存的管理信息     |
   | WWW-Authenticate   | 服务器对客户端的认证信息     |

10. 实体首部字段：

   | 首部字段名       | 说明                         |
   | ---------------- | ---------------------------- |
   | Allow            | 资源可支持的HTTP方法         |
   | Content-Encoding | 实体主体适用的编码方式       |
   | Content-Language | 实体主体的自然语言           |
   | Content-Length   | 实体主体的大小（单位：字节） |
   | Content-Location | 替代对应资源的URI            |
   | Content-MD5      | 实体主体的报文摘要           |
   | Content-Range    | 实体主体的位置范围           |
   | Content-Type     | 实体主体的媒体类型           |
   | Expires          | 实体主体过期的日期时间       |
   | Last-Modified    | 资源的最后修改日期时间       |

11. 























