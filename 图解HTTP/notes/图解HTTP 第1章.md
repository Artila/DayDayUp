### 图解HTTP 第一章

1. HTTP/1.0  1996.5 虽说是初期标准，但该协议标准至今仍被广泛使用在服务器端

2. HTTP/1.1 1997.1 目前主流的HTTP协议版本。

3. 可见，作为Web文档传输协议的HTTP，它的版本几乎没有更新。新一代HTTP/2.0 正在制订中。

4. 通常使用的网络（包括互联网）是在TCP/IP协议族的基础上运作的。而HTTP属于它内部的一个子集。

5. TCP/IP 是互联网相关的各类协议族的总称。

   ![TCP-IP.jpg](https://upload-images.jianshu.io/upload_images/1331173-2f6a3d689165cae0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 也有说法认为，TCP/IP 是指TCP和IP这两种协议。还有一种说法认为，TCP/IP 是在IP协议的通信过程中，使用到的协议族的统称。

7. TCP/IP协议族里重要的一点就是分层。TCP/IP协议族按层次分别分为以下4层：

   - 应用层：决定了向用户提供应用服务时通信的活动。HTTP 协议也处于该层。

   - 传输层：对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。

   - 网络层：又称网络互连层，用来处理在网络上流动的数据包。数据包是网络传输的最小数据单位。该层规定了通过怎样的路径（所谓的传输路线）到达对方计算机，并把数据包传送给对方。

     与对方计算机之间通过多台计算机或网络设备进行传输时，网络层所起的作用就是在众多的选项内选择一条传输路线。

   - 数据链路层：又名链路层，网络接口层，用来处理连接网络的硬件部分。包括控制操作系统、硬件的设备驱动、NIC（Network Interface Card，网络适配器，即网卡），及光纤等物理可见部分（还包括连接器等一切传输媒介）。硬件上的范畴均在链路层的作用范围之内。

8. 利用TCP/IP协议族进行网络通信时，会通过分层顺序与对方进行通信。发送端从应用层往下走，接收端则往应用层网上走。

  ![TCP-IP通信.jpg](https://upload-images.jianshu.io/upload_images/1331173-2180e55aa6c6431a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9. 发送端在层与层之间传输数据时，每经过一层时必定会被打上一个该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层时都会把对应的首部消去。

   这种把数据信息包装起来的做法成为封装（encapsulate）。

   ![封装.jpg](https://upload-images.jianshu.io/upload_images/1331173-0c4fb3528d2fb5e8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10. IP（Internet Protocol）网际协议位于网络层。

11. Internet Protocol 这个名称可能听起来有点夸张，但事实正是如此，因为几乎所有使用网络的系统都会用到IP协议。TCP/IP 协议族中的IP指的就是网际协议，协议名称中占据了一半位置，其重要性可见一斑。可能有人会“IP”和“IP地址”搞混，“IP”其实是一种协议的名称。

12. IP协议的作用是把各种数据包传送给对方。而要保证确实传送到对方那里，则需要满足各类条件。其中两个重要的条件是IP地址和MAC地址（Media Access Control Address）。

13. IP地址指明了节点被分配到的地址，MAC地址是指网卡所属的固定地址。IP地址可以和MAC地址进行配对。IP地址可变换，但MAC地址基本上不会更改。

14. IP间的通信依赖MAC地址。在网络上，通信的双方在同一局域网（LAN）内的情况是很少的，通常是指经过多台计算机和网络设备中转才能连接到对方。而在进行中转时，会利用下一站中转设备的MAC地址来搜索下一个中转目标。这时，会采用ARP协议（Address Resolution Protocol）。ARP是一种用以解析地址的协议，根据通信方的IP地址就可以反查出对应的MAC地址。

15. 在到达通信目标前的中转过程中，那些计算机和路由器等网络设备只能获悉很粗略的传输路线。这种机制称为路由选择（routing）。没有人能够全面掌握互联网中的传输状况。

16. TCP（Transmission Control Protocol）位于传输层，提供可靠的字节流服务。

17. 所谓的字节流服务（Byte Stream Service）是指，为了方便传输，将大块数据分割成以报文段（segment）为单位的数据包进行管理。

18. 而可靠的传输服务是指，能够把数据准确可靠地传给对方。一言以蔽之，TCP协议为了更容易传送大数据才把数据分割，而且TCP协议能够确认数据最终是否送达到对方。

19. 为了准确无误地将数据送达目标处，TCP协议采用了三次握手（three-way handshaking）策略。用TCP协议把数据包送出去后，TCP不会对传送后地情况置之不理，它一定会向对方确认是否成功送达。握手过程中使用了TCP地标志（flag）——SYN（synchronize）和ACK（acknowledgement）。

    发送端首先发送一个带SYN标志的数据包给对方。接收端收到后，回传一个带有SYN/ACK标志的数据包以示传达确认信息。最后，发送端再回传一个带ACK标志的数据包，代表“握手”结束。

    若在握手过程中某个阶段莫名中断，TCP协议会再次以相同的顺序发送相同的数据包。

    ![three-way handshaking.jpg](https://upload-images.jianshu.io/upload_images/1331173-0ccf75512e1e20a0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

20. 除了上述三次握手，TCP协议还有其他各种手段来保证通信的可靠性。

21. DNS（Domain Name System）服务是和HTTP协议一样位于应用层的协议。它提供域名到IP地址之间的解析服务。

22. 计算机既可以被赋予IP地址，也可以被赋予主机名和域名。比如：www.hackr.jp。

23. 用户通常使用主机名或域名来访问对方的计算机，而不是直接通过IP地址来访问。因为与IP地址的一组纯数字相比，用字母配合数字的表示形式来指定计算机名更符合人类的记忆习惯。

24. 但要让计算机去理解名称，相对而言就变得困难了。因为计算机更擅长处理一长串数字。

25. 为了解决上述的问题，DNS服务应运而生。DNS协议通过域名查找IP地址，或逆向从IP地址反查域名的服务。

    ![DNS.jpg](https://upload-images.jianshu.io/upload_images/1331173-592e2fa8adedbd13.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

26. 通过下图了解IP协议、TCP协议和DNS服务在使用HTTP协议的通信过程中各自发挥了哪些作用

    ![各种协议在通信过程中的作用.jpg](https://upload-images.jianshu.io/upload_images/1331173-553a46d384e3a11b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

27. 与URI（统一资源标识符）相比，我们更熟悉URL（Uniform Resource Locator，统一资源定位符）。URL正是使用Web浏览器等访问Web页面时需要输入的网页地址。

28. URI：Uniform Resource Identifier ，URI就是由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名称。

    采用HTTP协议时，协议方案就是http。除此之外，还有ftp、mailto、telnet、file等。

    标准的URI协议方案有30种左右，由隶属于国际互联网资源管理的非营利社团ICANN（Internet Corporation for Assigned  Names and Numbers，互联网名称与数字地址分配机构）的IANA（Internet Assigned Numbers Authority，互联网号码分配局）管理颁布。

29. URI 用字符串标识某一互联网资源，而URL表示资源的地点（互联网上所处的位置）。可见URL是URI的子集。

30. URI格式：表示指定的URI，要使用涵盖全部必要信息的绝对URI、绝对URL以及相对URL。

31. 相对URL：是指从浏览器中基本URI处指定的URL，形如`/image/logo.gif`。

32. 绝对URI：

    ![绝对URI.jpg](https://upload-images.jianshu.io/upload_images/1331173-43ec29d06170383b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    - 使用`http: `或 `https:` 等协议方案名获取访问资源时要指定协议类型。不区分字母大小写，最后附一个冒号（:）。
    - 也可使用 `data: `或` javascript: `这类指定数据或脚本程序的方案名。
    - 登录使用（认证）：指定用户名或密码作为从服务器端获取资源时必要的登录信息（身份认证）。此选项是可选项。
    - 服务器地址：使用绝对URI必须指定待访问的服务器地址。地址可以是类似`hackr.js`这种DNS可解析的名称，或是`192.168.1.1`这类IPv4地址名，还可以是`[0:0:0:0:0:0:0:1]`这样用方括号括起来的IPv6地址名。
    - 服务器端口号：指定服务器连接的网络端口号。此选项也是可选项，若用户省略则自动使用默认端口号。
    - 带层次的文件路径：指定服务器上的文件路径来定位特指的资源。这与UNIX系统的文件目录结构相似。
    - 查询字符串：针对已指定的文件路径内的资源，可以使用查询字符串传入任意参数。此项可选。
    - 片段标识符：使用片段标识符通常可标记出已获取资源中的子资源（文档内的某个位置）。但在RFC中并没有明确规定其使用方法。该项也为可选项。

33. 并不是所有的应用程序都符合RFC。

























