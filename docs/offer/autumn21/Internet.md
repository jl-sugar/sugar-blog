# 前端备战秋招之计算机网络

![图片](http://img.cdn.sugarat.top/mdImg/MTU4NTIzMzA2NDMwNw==585233064307)

## 常见协议的端口
![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzYyMTk2NTM4NQ==593621965385)

## OSI体系结构
自低向上(7层结构)
1. 物理层
2. 数据链路层
3. 网络层
4. 传输层
5. 会话层
6. 表现层
7. 应用层

TODO：贴生动形象图
## TCP/IP
自底向上（4层）
1. 网络接口层
2. 网络IP层
3. 运输层
4. 应用层

TODO：贴生动形象图

## 五层体协结构
自底向上
1. 物理层
2. 数据链路层
3. 网络层
4. 运输层
5. 应用层

TODO：贴生动形象图

## 网际层IP协议
<img style="background-color:white;" src="http://img.cdn.sugarat.top/mdImg/MTU5MzYxNzg5MDI1Ng==593617890256"/>

* ARP:地址解析协议--从网络层使用的 IP 地址，解析出在数据链路层使用的硬件地址
* ICMP：网际控制报文协议--用于在IP主机、路由器之间传递控制消息
  * ICMP 允许主机或路由器报告差错情况和提供有关异常情况的报告
  * ICMP 属于IP 层的协议
  * PING 使用了 ICMP 回送请求与回送回答报文
* IGMP：网际组管理协议--

### IP地址分类
| 类别  | 构成(x+网络号+主机号) |            范围            |     用途     |
| :---: | :-------------------: | :------------------------: | :----------: |
|   A   |       `0`+7+24        | 1.0.0.1---126.255.255.254  |              |
|   B   |      `10`+14+16       |  128.0.0.0---191.255.0.0   |              |
|   C   |      `110`+21+8       | 192.0.0.0--- 223.255.255.0 |              |
|   D   |   `1110`+ 28(多播)    |                            |   多播地址   |
|   E   |     `11110`+留用      |                            | 保留今后使用 |

### 通信类型
* 单播：从一台主机向另一台主机发送数据包的过程
* 组播：从一台主机向选定的一组主机发送数据包的过程
* 广播：从一台主机向该网络中的所有主机发送数据包的过程
  * A类、B类与C类IP地址中主机号全1的地址为直接广播地址

### IP数据报
#### 构成
* 首部
  * 前：固定长度20
  * 后：有可选字段，长度可变
* 数据

#### 图解构成
![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzYxOTgwNzUyNw==593619807527)

TODO：想办法巧妙记住

* 版本：4位--IP协议版本，等于4代表IPV4
* 首部长度：4位--可表示的最大数值15*4=60字节，因此 IP 的首部长度的最大值是 60 字节
* 区分服务：8位--用来获得更好的服务，在一般的情况下都不使用这个字段 
* 总长度：16位--首部和数据之和长度，单位字节，于是数据报的最大长度为65535字节 2^16-1
  * 总长度必须不超过最大传送单元 `MTU`
* 标识：16位--计数器，用来产生IP数据报的标识
* 标志：3位--目前只有前两位有意义
  * 最低位MF（More Fragment）：1--后面还有分片，0--为最后一个分片
  * 中间位DF（Don't Fragment）：0--才允许分片
* 片偏移：13位--指出：较长的分组在分片后，某片在原分组中的相对位置
  * 片偏移以 8 个字节为偏移单位
* 生存时间：8位--记为TTL（Time To Live），数据报在网络中可通过的路由器数的最大值
* 协议：8位--指出此数据报携带的数据使用何种协议
  * 以便目的主机的 IP 层将数据部分上交给那个处理过程
* 首部检验和：16位--只检验数据报的首部，不检验数据部分
  * 这里不采用 CRC 检验码而采用简单的计算方法
  * IP 数据报首部检验和的计算采用 16 位二进制反码求和算法
* 源地址：32位--4字节
* 目的地之：32位--4字节

![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzYyMDk2ODE1MQ==593620968151)

### PING
* PING 用来测试两个主机之间的连通性
* PING 使用了 ICMP 回送请求与回送回答报文
* PING 是应用层直接使用网络层 ICMP 的例子，它没有通过运输层的 TCP 或UDP

## 运输层
![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzYyMTYyOTYyMA==593621629620)
## UDP
用户数据报协议（User Datagram Protocol）
* 数据单位协议：UDP 报文或用户数据报
### 特点
* 无连接服务协议
  * 传送数据之前不需要建立连接
* 尽最大努力交付，不提供可靠交付
  * 数据报文的搬运工，不保证有序且不丢失的传递到对端
* 面向报文的
* 没有拥塞控制，没有流量控制算法
* 支持一对一、一对多、多对一和多对多的交互通信
* UDP 的首部开销小，只有 8 个字节，比 TCP 的 20 个字节的首部要短

### 面向无连接
* UDP 是不需要和 TCP 一样在发送数据前进行三次握手建立连接，想发数据就可以开始发送了
* 只是数据报文的搬运工，不会对数据报文进行任何拆分和拼接操作
  * 发送端：应用层将数据传递给传输层的 UDP 协议，UDP 只会给数据增加一个 UDP 头,表示用的是 UDP 协议，然后就传递给网络层了
  * 接收端：网络层将数据传递给传输层，UDP 只去除 IP 报文头就传递给应用层，不会任何拼接操作

### 不可靠性
* 不可靠性体现在无连接上
  * 通信不需要建立连接,想发就发
* 收到什么数据就发生什么数据,不对数据进行校验与备份
* 不关心发送端是否收到了数据
* 没有拥堵控制会以恒定的速度发送数据
  * 在网络条件不好的情况下会导致丢包

### 高效
* UDP 的首部开销小，只有 8 个字节，比 TCP 的 20 个字节的首部要少得多

![](http://img.cdn.sugarat.top/mdImg/MTU4MzIyMDM3OTg1MA==583220379850)

### 传输方式
* 一对多：单播
* 多对多：多播
* 多对一：广播

### 适合场景
对当前网络通讯质量要求不高的时候,实时性要求高的地方都可以看到 UDP 的身影，要求网络通讯速度尽量的快，这时就使用UDP
* 网游
* 直播
* 语音
* 视屏等等

### 数据报格式
![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzYyMjM0OTY4OA==593622349688)
* 源端口--16位
* 目的端口--16位
* 整个数据报文的长度--16位
* 检验和--16位该字段用于发现头部信息和数据中的错误

### 总结
* UDP 相比 TCP 简单的多，不需要建立连接，不需要验证数据报文，不需要流量控制，只会把想发的数据报文直接发送给对端
* 虽然 UDP 并没有 TCP 传输来的准确，但是也能在很多实时性要求高的地方有所作为

## TCP
传输控制协议（Transmission Control Protocol）
* 数据单位协议：TCP 报文段

### 特点
* 面向连接的运输层协议
* 每一条 TCP 连接只能有两个端点 (endpoint)，每一条 TCP 连接`只能是点对点`的（一对一）
* 提供可靠交付的服务
* 提供全双工通信
* 面向字节流
  * 但 TCP 传送的数据单元却是报文段
* TCP 不提供广播或多播服务
* 首部的前 20 个字节是固定的，后面有 4n 字节是根据需要而增加的选项 (n 是整数)
  * 因此 TCP 首部的最小长度是 20 字节

### 建立连接三次握手
>三报文握手主要是为了防止已失效的连接请求报文段突然又传送到了，因而产生错误。

![图片](http://img.cdn.sugarat.top/mdImg/MTU5Mzg0MzU4NzI2NQ==593843587265)

起初，两端都为 CLOSED 状态。在通信开始前，双方都会创建 TCB。 服务器创建完 TCB 后便进入 LISTEN 状态，此时开始等待客户端发送数据

1. 第一次握手
   * 客户端发送的SYN=1（同步序列号seq=x）的包到服务端并变为SYN-SENT（请求连接）状态，等待服务端响应
2. 第二次握手
   * 服务端收到客户端请求后，发送一个包（SYN=1，ACK=1，seq=y,ack=x+1）给客户发端，服务端进入SYN_RECEVIED状态
3. 第三次握手
   * 客户端收到服务端响应的包（SYN=1，ACK=1）后，再向服务端发送确认包（ACK=1，seq=x+1，ack=y+1），发送完毕，客户端和服务端都进入ESTABLISHED状态，完成握手

### 连接释放四次挥手
>数据传输结束后，通信的双方都可释放连接

![图片](http://img.cdn.sugarat.top/mdImg/MTU5Mzg0NTQwODY4Nw==593845408687)
TCP 是全双工的，在断开连接时两端都需要发送 FIN 和 ACK
1. 第一次挥手
   * 客户端认为数据发送完成，向服务端发送链接释放请求(FIN=1,序号seq=u)，等待服务端确认
2. 第二次挥手
   * 服务端收到请求后,通知应用层要释放 TCP 链接。然后会发出确认包（ACK =1，seq=V,ACK=u+1），并进入 CLOSE_WAIT 状态
     * 此时表明 客户端 到 服务端 的连接已经释放，不再接收 客户端 发的数据了
     * 但是因为 TCP 连接是双向的，此时处于半关闭状态服务端 仍旧可以发送数据给 客户端
     * 服务端如果此时还有没发完的数据会继续发送
3. 第三次挥手
   * 服务端发送完毕后向 客户端 发送连接释放请求(FIN=1,ACK=1,seq=w,ack=u+1),然后 服务端 便进入 LAST-ACK 状态
4. 第四次挥手
   * 客户端收到连接释放报文段后，向服务端发送确认应答
   * 然后 客户端 进入 TIME-WAIT 状态
     * 该状态会持续 2MSL（最大段生存期，指报文段在网络中生存的时间，超时会被抛弃） 时间，若该时间段内没有 B 的重发请求的话，就进入 CLOSED 状态。当 服务端 收到确认应答后，也便进入 CLOSED 状态。
### 首部格式
![图片](http://img.cdn.sugarat.top/mdImg/MTU5MzY1NDYwMDI2OQ==593654600269)
* 源端口：2字节
* 目的端口：2字节
  * 端口是运输层与应用层的服务接口。运输层的复用和分用功能都要通过端口才能实现
* 序号：4 字节
  * TCP 连接中传送的数据流中的每一个字节都编上一个序号
  * 序号字段的值则指的是本报文段所发送的数据的第一个字节的序号
  * 报文段的序号字段值=301，而携带的数据共有100字节，则本报文段的数据第一个字节序号是301，最后一个字节的序号是400.那么下一个报文段的数据序号应当是401
* 确认号：4 字节，是期望收到对方的下一个报文段的数据的第一个字节的序号
  * 若确认号=N 则表示：到序号N-1为止的所有数据都已正确收到
  * 如果接收方B收到A发送过来的报文段，序号=501，数据长度是200字节，表明B收到了A发送的到序号700为止的数据。则B发送给A的确认报文段中把确认号设置为701
* 数据偏移：4位，指出 TCP 报文段的数据起始处距离 TCP 报文段的起始处有多远
  * 单位是4字节
  * 实际上是TCP报文段的首部长度
  * 最大TCP报文段首部=60字节=(2^4-1)*4
* 保留字段：6 位，保留为今后使用
  * 目前应置为 0 
* URG：1位，紧急（urgent）
  * 当 URG为1 时，表明紧急指针字段有效，它告诉系统此报文段中有紧急数据，应尽快传送(相当于高优先级的数据) 
* ACK：1位，确认（acknowledge）
  * ACK=1时确认号才有效
* PSH：1位，推送（push）
  *  PSH = 1 的报文段，就尽快地交付接收应用进程，而不再等到整个缓存都填满了后再向上交付
* RST：1位，复位（reset）
  * RST=1，TCP 连接中出现严重差错（如由于主机崩溃或其他原因），必须释放连接，然后再重新建立运输连接
* SYN：1位，同步（synchronous）
  *  SYN = 1 表示这是一个连接请求或连接接受报文
     *  SYN=1 ACK=0: 连接请求报文段
     *  SYN=1 ACK=1：连接接收报文段
* FIN：1位，终止（finish）
  * FIN = 1 表明此报文段的发送端的数据已发送完毕，并要求释放运输连接
* 窗口字段：2 字节-窗口是发送本报文段的一方的接收窗口，是用来让对方设置发送窗口的依据
  * 如确认号=701，窗口字段=1000，则表示告诉对方：从701号开始，我的接收缓存还可以接收1000字节
* 检验和：2 字节，检验和字段检验的范围包括首部和数据这两部分
  * 在计算检验和时，要在 TCP 报文段的前面加上 12 字节的伪首部
* 紧急指针字段：2字节，指出在本报文段中紧急数据共有多少个字节（紧急数据放在本报文段数据的最前面）
* 选项字段：长度可变
  * TCP 最初只规定了一种选项，即最大报文段长度 MSS
    * MSS 告诉对方TCP：“我的缓存所能接收的报文段的数据字段的最大长度是 MSS 个字节。”
    * 数据字段加上 TCP 首部才等于整个的 TCP 报文段
    * 所以，MSS是“TCP 报文段长度减去 TCP 首部长度”
* 填充字段：这是为了使整个首部长度是 4 字节的整数倍

### 可靠传输工作原理
#### 停止等待ARQ
每发送完一个分组就停止发送，等待对方的确认。在收到确认后再发送下一个分组。

#### 连续ARQ
发送方维持的发送窗口，它的意义是：位于发送窗口内的分组都可连续发送出去，而不需要等待对方的确认。这样，信道利用率就提高了

连续 ARQ 协议规定，发送方每收到一个确认，就把发送窗口向前滑动一个分组的位置。

#### 流量控制
>流量控制所要做的就是抑制发送端发送数据的速率，以便使接收端来得及接收

利用滑动窗口实现流量控制

#### 拥塞控制
>拥塞控制就是防止过多的数据注入到网络中，使网络中的路由器或链路不致过载

* TCP 采用基于窗口的方法进行拥塞控制。该方法属于闭环控制方法。
* TCP发送方维持一个拥塞窗口 CWND
  * 拥塞窗口的大小取决于网络的拥塞程度，并且动态地在变化。
  * 发送端利用拥塞窗口根据网络的拥塞情况调整发送的数据量。
  * 所以，发送窗口大小不仅取决于接收方公告的接收窗口，还取决于网络的拥塞状况，所以真正的发送窗口值为：min（公告窗口值，拥塞窗口值）

拥塞的判断
* 重传定时器超时
* 收到三个相同重复的ACK

四种控制算法
* 慢开始：由小到大逐渐增大拥塞窗口数值
* 拥塞避免：让拥塞窗口 cwnd 缓慢地增大，即每经过一个往返时间 RTT 就把发送方的拥塞窗口 cwnd 加 1，而不是加倍，使拥塞窗口 cwnd 按线性规律缓慢增长
* 快重传：让发送方尽早知道发生了个别报文段的丢失
  * 发送方只要一连收到三个重复确认，就知道接收方确实没有收到报文段，因而应当立即进行重传
* 快恢复：当发送端收到连续三个重复的确认时，由于发送方现在认为网络很可能没有发生拥塞，因此现在不执行慢开始算法，而是执行快恢复算法

### 适合场景
* HTTP
* FTP
* SMTP
* 文件传输
* 游戏。。。

## TCP与UDP相关问题
### 1.为什么 TCP 建立连接需要三次握手，明明两次就可以建立起连接？
* 防止出现失效的连接请求报文段被服务端接收的情况，从而产生错误
* 如果只有1次：客户端收到请求后，没收到应答，无法判断链接是否连接成功
* 如果只有2次：
  * 客户端发送连接请求后，等待服务器端的应答。
  * 如过客户端的SYN过了一段时间没有到达服务器端，客户端链接超时，会重新发送一次连接请求
  * 如果重发的这次服务器端收到了，且应答了客户端，连接就建立了
  * 但是建立后，第一个SYN也到达服务端了，这时服务端会认为这是一个新连接，会再给客户端发送一个ACK，这个ACK当然会被客户端丢弃
  * 但是此时服务器端已经为这个连接分配资源了，而且服务器端会一直维持着这个资源，会造成浪费

### 2.三次握手过程中可以携带数据么？
* 第三次可以携带
  * 客户端已经处于ESTABLIEISH状态，已经能够确认服务端的接收，发送能力正常，这个时候可以携带
* 前两次不可以
  * 一旦有人想攻击服务器，只需要在第一次握手中的 SYN 报文中放大量数据，那么服务器会消耗更多的时间和内存空间去处理这些数据，增大了服务器被攻击的风险

### 3.为什么 A 要进入 TIME-WAIT 状态，等待 2MSL 时间后才进入 CLOSED 状态
>MSL -- Maximum Segment Lifetime -- 报文最大生存时间,最长报文寿命

1. 为了保证 客户端 发送的最后一个 ACK 报文段能够到达 服务端
2. 防止 “已失效的连接请求报文段”出现在本连接中
   * 若 客户端 发完确认应答后直接进入 CLOSED 状态，如果确认应答因为网络问题一直没有到达，那么会造成 服务端 不能正常关闭。
   * 如果不等待客户端直接关闭，当服务端还有数据包要发送给客户端时，且还在传输的路上，若客户端的端口此时刚好被新的应用占用，那么就接收到了无用数据包，造成数据包混乱
3. 2MSL意义:
   * 1 个 MSL 确保四次挥手中主动关闭方最后的 ACK 报文最终能达到对端
   * 1 个 MSL 确保对端没有收到 ACK 重传的 FIN 报文可以到达
   * 经过2MSL,可以使本链接持续时间内所产生的所有报文段,都从网络中消失

### 4.TCP与UDP的区别
* UDP 协议是面向无连接的:不需要在正式传递数据之前先连接起双方
* UDP 协议只是数据报文的搬运工:不保证有序且不丢失的传递到对端
* UDP 协议也没有任何控制流量的算法
* UDP 相较于 TCP 更加的轻便
* UDP 的首部开销小，只有 8 个字节，比 TCP 的 20 个字节的首部要少得多

* TCP面向连接的
* 基本与UDP反着来
* 建立连接3次握手
* 断开连接4次挥手
* 通过各种算法保持保证传输的可靠性

## HTTP
超文本传输协议(HyperText Transfer Protocol）),基于TCP实现的应用层协议
### 特点
* 请求响应模型:客户端发送请求,服务端响应请求
* 无状态协议:不需要建立持久链接

### 工作过程
1. 地址解析
2. 封装HTTP请求数据包
3. 封装成TCP包，建立TCP链接
4. 客户端发送请求
5. 服务端响应
6. 关闭TCP链接
   * 保持链接的方案:在请求/响应头中加入 `Connection:keep-alive`就可以保持链接打开状态

### 请求构成
* 请求行
* 首部
* 实体

### 响应构成
* 协议/版本号 状态码 
* 首部
* 实体

### 请求行
GET /images/logo.gif HTTP/1.1

由请求方法、URL、协议版本组成

### 请求方法
>请求方法分为很多种，最常用的也就是 Get 和 Post 了。虽然请求方法有很多，但是更多的是传达一个语义，而不是说 Post 能做的事情 Get 就不能做了
* Get:应该只被用于获取数据
* Post:用于将实体提交到指定的资源，通常导致在服务器上的状态变化或副作用.
* Put:求有效载荷替换目标资源的所有当前表示,即更新操作.
* Delete:删除指定的资源
* Patch:用于对资源应用部分修改
* Head:请求一个与GET请求的响应相同的响应，但没有响应体.
* Connect:建立一个到由目标资源标识的服务器的隧道
* Options:描述目标资源的通信选项
* Trace:沿着到目标资源的路径执行一个消息环回测试。

### URI
`Uniform Resource Identifier`--统一资源标识符,用于区分互联网上不同资源

`URI` 包含 `URL` 与 `URN`

![图片](http://img.cdn.sugarat.top/mdImg/MTU5Mzg1NDQzMjQ4NQ==593854432485)

URI只能使用ASCII, ASCII 之外的字符不支持显示,因此，URI 引入了编码机制，将所有非 ASCII 码字符和界定符转为十六进制字节值，然后在前面加个%

### URL
>scheme://host:port/path?query
  
* scheme:协议,HTTP,HTTPS,FTP
* host:主机名,sugarat.top
* port:端口号,默认80,https默认443
* path:资源路径
* query:用于查询的参数

### URN
>path?query

### 副作用和幂等
* 副作用:指对服务器上的资源做改变
  * 搜索是无副作用的，注册是副作用

* 幂等:指发送 M 和 N 次请求（两者不相同且都大于 1）
  * 服务器上资源的状态一致，比如注册 10 个和 11 个帐号是不幂等的
  * 对文章进行更改 10 次和 11 次是幂等的。因为前者是多了一个账号（资源），后者只是更新同一个资源。

### 常见首部
#### 通用首部
|       字段        |                     作用                      |
| :---------------: | :-------------------------------------------: |
|   Cache-Control   |                控制缓存的行为                 |
|    Connection     | 浏览器想要优先使用的连接类型，比如 keep-alive |
|       Date        |                 创建报文时间                  |
|      Pragma       |                   报文指令                    |
|        Via        |              代理服务器相关信息               |
| Transfer-Encoding |                 传输编码方式                  |
|      Upgrade      |              要求客户端升级协议               |
|      Warning      |             在内容中可能存在错误              |

#### 请求首部
|      字段       |                  作用                  |
| :-------------: | :------------------------------------: |
|      Host       |          访问资源所在的主机名          |
|     Accept      | 能正确接收的媒体类型(application/json) |
| Accept-Charset  |           能正确接收的字符集           |
| Accept-Encoding |     能正确接收的编码格式列表(gzip)     |
|   User-Agent    |          发送请求的客户端信息          |
|     Referer     |        浏览器所访问的前一个页面        |
| Accept-Language |  能正确接收的语言列表(zh-CN, zh, en)   |
|    If-Match     |    值与请求资源ETag相同才会处理请求    |
|  If-None-Match  |   值与请求资源ETag不相同才会处理请求   |

#### 响应首部
|        字段        |               作用               |
| :----------------: | :------------------------------: |
|        Age         |    资源在代理缓存中存在的时间    |
|       Server       |            服务器名字            |
|   Content-Length   |        告知客户端资源长度        |
|      Expires       |      告知客户端资源失效日期      |
|   Last-Modified    | 告知客户端资源最后一次修改的时间 |
|       E-tag        |     文件指纹，资源唯一标识符     |
|      Location      |      客户端重定向到某个 URL      |
| Proxy-Authenticate |     向代理服务器发送验证信息     |

#### cookie
|    字段    |           作用           |
| :--------: | :----------------------: |
|   Cookie   |    请求时携带的cookie    |
| Set-Cookie | 响应时服务端传回的cookie |

#### 压缩相关
|       字段       |         作用         |
| :--------------: | :------------------: |
| Content-Encoding | 发送端使用的编码方式 |
| Accept-Encoding  | 接收端支持的编码格式 |

### 状态码
**1xx协议处理的中间状态**
* ``101`` 在HTTP升级为WebSocket的时候，如果服务器同意变更，就会发送状态码 101

**2xx成功**
* ``200`` 客户端的请求被服务端正确处理
* ``204`` 请求成功但响应报文不包含实体的主体部分
* 206 范围请求,客户端进行了部分请求,服务端返回指定部分的内容
* 205 与204作用一致但要求请求方重置内容

**3xx重定向**
* ``301`` 永久性重定向,表示资源已被分配了新的url
* ``302`` 临时性重定向,表示资源临时被分配了新的url
* ``304`` 当客户端拥有可能过期的缓存时，会携带缓存的标识 etag、时间等信息询问服务器缓存是否仍可复用，而304是告诉客户端可以复用缓存
* 303 资源存在另一个url,服务端要求客户端使用get请求
* 307 临时重定向,向新的url发送同样的请求

**4XX客户端错误**
* ``400`` 请求报文存在语法错误
* ``401`` 发送的请求需要有通过 HTTP 认证的认证信息
* ``403`` 对请求资源的访问被服务器拒绝,资源允许访问,但请求不满足条件
* ``404`` 在服务器上没有找到请求的资源
* ``405`` 当前的请求方法不被允许
* ``415`` 不支持的媒体类型,检查Content-Type

**5XX 服务器错误**
* ``500`` 服务器端在收到请求后后，执行相关动作时发生了错误
* ``502`` bad gate无效网关
* 501 表示服务器不支持当前请求所需要的某个功能
* 503 表明服务器暂时处于超负载或正在停机维护，无法处理请求

### 缺点
* 通信使用明文，可能被窃听
* 不验证通信方的身份，可能遭遇伪装
* 无法证明报文的完整性，有可能遭遇篡改

## HTTPS
HTTP + 加密 + 认证 + 完整性保护 = HTTPS

* 基于HTTP协议，通过SSL或TLS协议提供加密处理数据、验证对方身份以及数据完整性保护
* 在HTTP上建立SSL加密层，并对传输数据进行加密，是HTTP协议的安全版
### 特点
通过抓包获取到的数据不是明文传输的
* 内容加密：采用混合加密技术，中间者无法直接查看明文内容
* 验证身份：通过证书认证客户端访问的是自己的服务器
* 保护数据完整性：防止传输的内容被中间人冒充或者篡改
### 缺点
* 性能损耗
* 增加延时
* 消耗较多的CPU资源

### 优化方案
* CDN
* 会话缓存

## TLS/SSL
>TLS是传输层加密协议，前身是SSL协议

TLS 协议位于传输层之上，应用层之下

HTTPS 还是通过了 HTTP 来传输信息，但是信息通过 TLS 协议进行了加密

### 功能实现
利用非对称加密实现身份认证和密钥协商，采用对称加密算法协商的密钥对数据加密，基于散列函数验证信息的完整性

* 散列函数 Hash:MD5,SHA,SHA256---完成校验
* 对称加密 1-1:AES,DES,RC4---信息加密
* 非对称加密 1-N:RSA,ECC,DH---身份验证秘钥协商

#### 对称加密
对称加密就是两边拥有相同的秘钥，两边都知道如何将密文加密解密。

这种加密方式固然很好，但是问题就在于如何让双方知道秘钥。因为传输数据都是走的网络，如果将秘钥通过网络的方式传递的话，一旦秘钥被截获就没有加密的意义的。

#### 非对称加密
有公钥私钥之分，公钥所有人都可以知道，可以将数据用公钥加密，但是将数据解密必须使用私钥解密，私钥只有分发公钥的一方才知道。

这种加密方式就可以完美解决对称加密存在的问题。假设现在两端需要使用对称加密，那么在这之前，可以先使用非对称加密交换秘钥。

简单流程如下：首先服务端将公钥公布出去，那么客户端也就知道公钥了。接下来客户端创建一个秘钥，然后通过公钥加密并发送给服务端，服务端接收到密文以后通过私钥解密出正确的秘钥，这时候两端就都知道秘钥是什么了。

### TLS1.2握手过程
1. 客户端发出请求:
   * 一个随机值(用于生成对话秘钥)
   * 支持的协议
   * 支持加密方式
   * 支持压缩的方法
2. 服务端收到客户端的请求，向客户端发出回应:
   * 一个随机值(用于生成对话秘钥)
   * 确定使用的协议
   * 确定使用的加密方式
   * 发送自己的证书（如果需要验证客户端证书需要说明）
3. 客户端收到服务端的证书并验证是否有效，如果证书没问题,向服务端发送一个请求:
   * 生成一个随机值(用证书公钥加密)
   * 编码改变通知(随后的信息将使用双方商定的加密方法和秘钥发送)
   * 客户端握手结束通知(前面发送的所有内容的hash值，用来提供给服务端校验)
4. 服务端最后响应
   * 服务器收到客户端的第三个随机数之后(用私钥解密)结合之前的两个明文随机数，计算生成本次会话所用的"会话密钥"
   * 编码改变通知(随后的信息都将用双方商定的加密方法和密钥发送)
   * 服务器握手结束通知(前面发送的所有内容的hash值，用来提供给客户端校验)

通过以上步骤可知，在 TLS 握手阶段，两端使用非对称加密的方式来通信，实现身份验证并协商对称加密使用的密钥,但是因为非对称加密损耗的性能比对称加密大，所以在正式传输数据时，两端使用对称加密的方式通信。不同的节点之间采用的对称密钥不同，从而可以保证信息只能通信双方获取

### TLS1.3
TLS1.3 中废除了非常多的加密算法,如果私钥泄露,那么中间人可以破解所有密文

TLS1.3 在 TLS1.2 的基础上废除了大量的算法，提升了安全性。同时利用会话复用节省了重新生成密钥的时间，利用 **PSK** 做到了0-RTT连接

## HTTP2
HTTP/2 相比于 HTTP/1，大幅度提高了网页的性能

在 HTTP/1 中,浏览器限制了同一个域名下的请求数量（Chrome 下一般是限制六个连接）

当页面中需要请求很多资源的时候，队头阻塞（Head of line blocking）会导致在达到最大请求数量时，剩余的资源需要等待其他资源请求完成后才能发起请求

### 特点
* HTTP/2 中引入了多路复用的技术，这个技术可以只通过一个 TCP 连接就可以传输所有的请求数据。多路复用很好的解决了浏览器限制同一个域名下的请求数量的问题，同时也间接更容易实现全速传输
* 在之前的 HTTP 版本中，我们是通过文本的方式传输数据。在 HTTP/2 中引入了新的编码机制，所有传输的数据都会被分割，并采用二进制格式编码。

### 多路复用
在 HTTP/2 中，有两个非常重要的概念，分别是:
* **帧（frame）** 代表最小的数据单位，每个帧会标识出该帧属于哪个流
* **流（stream）** 是多个帧组成的数据流

多路复用，就是在一个 TCP 连接中可以存在多条流。换句话说，也就是可以发送多个请求，对端可以通过帧中的标识知道属于哪个请求。

通过这个技术，多个请求共享一个TCP连接，可以避免 HTTP 旧版本中的队头阻塞问题，极大的提高传输性能

### Header 压缩
在 HTTP/1 中，我们使用文本的形式传输 header，在 header 携带 cookie 的情况下，可能每次都需要重复传输几百到几千的字节。

在 HTTP /2 中，使用了 HPACK 压缩格式对传输的 header 进行编码，减少了 header 的大小。并在两端维护了索引表，用于记录出现过的 header ，后面在传输过程中就可以传输已经记录过的 header 的键名，对端收到数据后就可以通过键名找到对应的值

### 服务端 Push
在 HTTP/2 中，服务端可以在客户端某个请求后，主动推送其他资源。

可以想象以下情况，某些资源客户端是一定会请求的，这时就可以采取服务端 push 的技术，提前给客户端推送必要的资源，这样在使用的时候就可以相对减少一点延迟时间。

### 设置请求优先级
* 可在新建的流所传递HEADERS帧中包含优先级priority属性
* 可单独通过PRIORITY帧专门设置流的优先级属性

### 使用前置条件
* 支持HTTP2的客户端与服务端
* 域名必须支持HTPPS协议（基于TLS/1.2或以上版本的加密连接）
* 服务器的openssl版本必须大于1.0.2

可通过Nginx搭建HTTP2服务器

## HTTP3
HTTP/2 使用了多路复用

一般来说同一域名下只需要使用一个 TCP 连接。当这个连接中出现了丢包的情况，那就会导致 HTTP/2 的表现情况反倒不如 HTTP/1 了
* 出现丢包的情况下，整个 TCP 都要开始等待重传，也就导致了后面的所有数据都被阻塞了
* 对于 HTTP/1 来说，可以开启多个 TCP 连接，出现这种情况反到只会影响其中一个连接，剩余的 TCP 连接还可以正常传输数据

基于这个原因，Google 就更起炉灶搞了一个基于 UDP 协议的 QUIC 协议，并且使用在了 HTTP/3 上
### QUIC
QUIC 基于 UDP，在原本的基础上新增了很多功能
* 多路复用
* 0-RTT
* 使用TLS1.3加密
* 流量控制
* 有序交付
* 重传
* 。。。

一种全新的基于UDP的web开发协议。可以用一个公式大致概括：

**TCP + TLS + HTTP2 = UDP + QUIC + HTTP2’s API**

QUIC协议虽然是基于UDP，但它不但具有TCP的可靠性、拥塞控制、流量控制等，且在TCP协议的基础上做了一些改进，比如避免了队首阻塞；

另外，QUIC协议具有TLS的安全传输特性，实现了TLS的保密功能，同时又使用更少的RTT建立安全的会话。

### 多路复用
**无队头阻塞的多路复用**

QUIC 原生实现了这个功能，并且传输的单个数据流可以保证有序交付且不会影响其他的数据流，这样的技术就解决了之前 TCP 存在的问题

QUIC 在移动端的表现也会比 TCP 好:
* 因为 TCP 是基于 IP 和端口去识别连接的，这种方式在多变的移动端网络环境下是很脆弱的
* QUIC 是通过 ID 的方式去识别一个连接，不管你网络环境如何变化，只要 ID 不变，就能迅速重连上

### 0-RTT
#### 与其他协议比较
* TCP建立链接需要三次握手，每次连接需要额外的RTT
* HTTPS加入了TLS还需要额外的RTT

#### 0-RTT情况
通过使用类似 TCP 快速打开的技术，缓存当前会话的上下文，在下次恢复会话的时候，只需要将之前的缓存传递给服务端验证通过就可以进行传输了

#### 1-RTT情况
新的QUIC连接至少需要1 RTT才能完成握手

![图片](http://img.cdn.sugarat.top/mdImg/MTU4NDMyMzc2NTY2MA==584323765660)

### 纠错机制
假如说这次我要发送三个包，那么协议会算出这三个包的异或值并单独发出一个校验包，也就是总共发出了四个包

当出现其中的非校验包丢包的情况时，可以通过另外三个包计算出丢失的数据包的内容。

当然这种技术只能使用在丢失一个包的情况下，如果出现丢失多个包就不能使用纠错机制了，只能使用重传的方式了

## 结构对比图
![图片](http://img.cdn.sugarat.top/mdImg/MTU4NTcxMzIwNDc0Nw==585713204747)

## 总结HTTP/2|3
* HTTP/2 通过多路复用、二进制流、Header 压缩等等技术，极大地提高了性能，但是还是存在着一定的问题的
* QUIC 基于 UDP 实现，是 HTTP/3 中的底层支撑协议，该协议基于 UDP，又取了 TCP 中的精华，实现了即快又可靠的协议，但目前兼容性并不好

## HTTP相关问题
### 1.POST和GET区别
#### 使用场景上区分
* GET多用于无副作用，幂等
* POST多用于有副作用，不冪等

#### 技术上
* GET会缓存，POST不会缓存
* GET请求参数会出现在url中，post相对安全一点
* URL有长度限制，会影响GET请求（浏览器规定）
* POST支持更多的编码类型，且不对数据做限制
* GET只能进行URL编码，只能接受ASCII字符

### 2.HTTP与HTTPS区别
* 安全：HTTP明文传输数据，HTTPS是在HTTP上建立SSL/TLS加密层，并对传输数据进行加密，更加安全
* 端口：http使用80端口，https使用443
* 速度：HTTP页面响应速度更快
  * HTTP只需建立TCP连接，发送3个包
  * HTTPS还需要经历TLS握手9个包需要，一共12个

### 3.HTTP1.1 如何解决 HTTP 的队头阻塞问题？
1. 域名分片：使用多个指向同一服务器的二级域名
2. 并发连接：也就是同时对一个域名发起多个长连接，用数量来解决质量的问题
   1. 浏览器一般会有限制

### 4.如果响应头Content-Length=0那么是发出来被截取了还是没发出来
结论：发出来被截取了

* Content-Length比实际的长度大, 服务端/客户端读取到消息结尾后, 会等待下一个字节,无响应直到超时
* Content-Length < 实际长度:首次请求的消息会被截取
* Content-Length如果存在且生效, 必须是正确的, 否则会发生异常
* 如果报文中包含Transfer-Encoding: chunked首部, 那么Content-Length将被忽略.

<comment/>
<tongji/>