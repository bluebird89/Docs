## Transmission Control Protocol/Internet Protocol TCP/IP 传输控制协议/网际协议
#computer #network

- 一个由 FTP、SMTP、TCP、UDP、IP 等协议构成的协议簇， 因为在TCP/IP协议中TCP协议和IP协议最具代表性，所以被称为TCP/IP协议
- 通信过程对应着数据入栈与出栈过程,供已连接因特网的计算机进行通信的通信协议.定义了电子设备（比如计算机）如何连入因特网，以及数据如何在它们之间传输的标准。包含了一系列构成互联网基础的网络协议，是Internet的核心协议
  - 入栈:数据发送方每层不断地封装首部与尾部，添加一些传输的信息，确保能传输到目的地
  - 出栈:数据接收方每层不断地拆除首部与尾部，得到最终传输的数据
- 对于多层次协议栈。每个层次都有各自端点（进行通讯的主体）
  - 处于同一层次两个端点使用该层次协议进行通讯
  - 除了最顶层，每个层次端点会向其直接上层提供服务
  - 除了最底层，每个层次端点会调用直接下层提供服务

## 概念

- 物理信道 直接使用某种物理介质来传送信息
- 逻辑信道 基于“物理信道”之上抽象出来的
- 带宽 信道在单位时间内最大能传输多少比特信息
  - 1Kbps  1000比特每秒
  - 1KiBps  1024字节每秒
- 单工 simplex 比如“电台广播”可以发信号给“收音机”，但“收音机”不能发信号给电台
- 半双工 half-duplex 比如“单条铁路轨道”，火车在单条铁轨上，可以有两种运行方向；但对于同一个瞬间，只能选其中一个方向（否则就撞车了）
- 全双工 full-duplex 比如“光纤”,在同一根光导纤维中，可以有多个光束同时相向传播，互相不会干扰对方
- RTT round-trip time which is the time it takes for a small packet to travel from client to server and back to the client.”
  - RTT=  packet-propagation delays 传播时延（往返）+  packet-queuing delays 排队时延（路由器和交换机的）+ packet -processing delay 数据处理时延（应用程序的）
- Throughput 吞吐量

## OSI Open Systems Interconnection Model

- 从上往下，越底层越接近硬件，越往上越接近软件的一个标准
- 计算机与网络传输：每层进行层层解包和附加自己所要传递信息，术语叫做报头
- Application(Layer 7) 7层应用层
  - This layer supports application and end-user processes. Communication partners are identified, quality of service is identified, user authentication and privacy are considered, and any constraints on data syntax are identified. Everything at this layer is application-specific. This layer provides application services for file transfers, e-mail, and other network software services.
  - 为应用软件提供接口，使应用程序能够使用网络服务
  - 打包请求，封装请求头和请求参数，应用层包通过 Socket 编程交到下一层去完成
  - DHCP, DNS, FTP, HTTP, IMAP4, NNTP, POP3, SMTP, SNMP, SSH, TELNET and NTP
- Presentation(Layer 6)   6层表示层
  - This layer provides independence from differences in data representation (e.g., encryption) by translating from application to network format, and vice versa. This layer formats and encrypts data to be sent across a network, providing freedom from compatibility problems. It is sometimes called the syntax layer.
  - 数据的解码和编码，加密和解密，压缩和解压缩
  - SSL, WEP, WPA, Kerberos   ASCLL、PICT、TIFF、JPEG、 MIDI、MPEG
- Session(Layer 5) 5层会话层
  - This layer establishes, manages and terminates connections between applications. The session layer sets up, coordinates, and terminates conversations, exchanges, and dialogues between the applications at each end. It deals with session and connection coordination.
  - 通过传输层（端口号：传输端口与接收端口）建立数据传输通路。
  - 主要在系统之间发起会话或或者接受会话请求（设备之间需要互相认识可以是IP也可以是MAC或者是主机名）
  - RPC、SQL、NFS 、X WINDOWS、ASP
- Transport(Layer 4) 4层传输层
  - This layer provides transparent transfer of data between end systems, or hosts, and is responsible for end-to-end error recovery and flow control. It ensures complete data transfer.
  - 负责建立端到端的链接，保证保温在端到端之间的传输
  - 数据 段|Segment
  - TCP, SPX and UDP
- Network(Layer 3) 3层网络层
  - This layer provides switching and routing technologies, creating logical paths, known as virtual circuits, for transmitting data from node to node. Routing and forwarding are functions of this layer, as well as addressing, internetworking, error handling, congestion control and packet sequencing.
  - 负责将分组数据从源端传输到目的端，网络层的主要作用就是路由和寻址
  - 数据 数据包|Packet
  - 路由器　Routers
  - IPv4, IPV6, IPX, OSPF, ICMP, IGMP and ARPMP
- Data Link(Layer 2)  2层数据链路层
  - At this layer, data packets are encoded and decoded into bits. It furnishes transmission protocol knowledge and management and handles errors in the physical layer, flow control and frame synchronization. The data link layer is divided into two sublayers:
  - The Media Access Control (MAC) layer   controls how a computer on the network gains access to the data and permission to transmit it.
  - the Logical Link Control (LLC) layer  controls frame synchronization, flow control and error checking.
  - 在不可靠的物理链路上，提供可靠的数据传输服务
  - 数据帧|Frame
  - 交换机、网桥、网卡
  - SLIP，CSLIP，PPP，ARP，RARP，MTU
  - 802.11 (WLAN), Wi-Fi, WiMAX, ATM, Ethernet, Token Ring, Frame Relay, PPTP, L2TP and ISDN-ore
- Physical(Layer 1)  1层物理层
  - This layer conveys the bit stream - electrical impulse, light or radio signal -- through the network at the electrical and mechanical level. It provides the hardware means of sending and receiving data on a carrier, including defining cables, cards and physical aspects.
  - 利用传输介质为数据链路层提供物理连接，实现比特流的透明传输
  - 数据 比特
  - 集线器 Hubs、中继器 Repeaters, Cables, Optical Fiber, SONET/SDN,Coaxial Cable, Twisted Pair Cable and Connectors (more)
  - ISO2110，IEEE802
- layers aims
  OSI Layer 1 is the physical medium carrying the 1’s and 0’s across the wire
  OSI Layer 2 is responsible for hop to hop delivery and uses MAC addresses
  OSI Layer 3 is responsible for end to end delivery and uses IP Addresses
  OSI Layer 4 is responsible for service to service delivery and uses Port Numbers
- services
  - Switches facilitate communications within networks and operate at Layer 2
  - Routers facilitate communication between networks and operate at Layer 3
  - ARP uses a known IP address to resolve an unknown MAC address

![OSI 协议模型](../_static/osi.png "OSI 协议模型")
![OSI 七层协议模型](../_static/osi_model.png "OSI 七层协议模型")
![七层协议](../_static/osi_1.png "Optional title")
![数据流](../_static/osi2.jpeg "Optional title")

## TCP/IP 协议模型

- 应用层
  - 决定向用户提供应用服务时通信的活动 HTTP curl SSH FTP
- 传输层
  - 提供处于网络连接中的两台计算机之间的数据传输  TCP UDP telent
  - 收到应用层数据(HTTP 请求报文)进行分割,并在各个报文上打上标记序号及端口号后转发给网络层
  - MAC地址 + IP + port
- 网络层
  - 数据包是网络传输的最小数据单位
  - 处理在网络上流动的数据包,与对方计算机之间通过多台计算机或网络设备进行传输时,网络层所起作用就是在众多的选项内选择一条传输路线
  - 规定通过怎样的路径(传输路线)到达对方计算机,并把数据包传送给对方
  - 增加作为通信目的地的 MAC 地址后转发给链路层 MAC地址+IP地址
- 以太网 数据链路层+物理层 用来处理连接网络的硬件部分
  - 包括控制操作系统、硬件的设备驱动、NIC(Network Interface Card,网络适配器,即网卡),及光纤等物理可见部分(还包括连接器等一切传输媒介)

![Alt text](../_static/tcp_ip.gif "Optional title")

## 数据流动

- 应用程序准备好数据，调用  `write()`  系统调用发送数据。假设所用 socket合法，发起系统调用后，发送流程切换到 kernel area
- 内核中每个 socket 有两个 buffer
  - send socket buffer 发送缓冲区
  - receive socket buffer 接收缓冲区
- 待发送数据从用户空间复制到内核内存中，然后添加进发送缓冲区的链表末尾。这样就可以按顺序发出数据
- 调用TCP/IP协议栈。每个 tcp 类型 socket 有一个TCP Control Block(TCB) 数据结构
  - TCB 包括一个TCP连接所需要的成员，比如 connection state 连接状态（LISTEN, ESTABLISHED, TIME_WAIT等）、receive window 接收窗口，congestion window 拥塞窗口、sequence number 包序号和 resending timer 重传定时器等。
  - 可以认为一个TCB 代表一条TCP连接。
- 如果当前 TCP 状态允许数据传输，会新建一个TCP segment
- TCP 报文进入下一层IP层处理，添加IP头部和checksum
  - IP路由选择 选择下一跳的过程
  - 将数据包发送到下一层Ethernet层，即数据链路层。
- Ethernet 层采用 ARP 协议搜索查询下一跳 IP 的MAC地址，然后向报文添加Ethernet 头部，host 部分报文处理完毕
- 调用 NIC 驱动(运行在 host 和内核的驱动程序，硬件是 CPU)发送数据
- NIC 驱动程序通过厂商制定的网卡与主机的通信协议向 NIC 请求发送 packet
  - NIC 收到发送网络包请求后，将报文复制到自己内存中然后发送到网络
  - NIC 发出一个数据包向 CPU 发出中断，每个中断有其自己的中断号，操作系统根据中断号调用对应的驱动程序处理中断
  - 驱动的中断处理函数是NIC驱动在OS启动时注册中断回调函数；当中断发生时，OS调用中断服务程序，然后中断服务程序向OS返回发送完成的数据包

![数据流](../_static/osi_data_flow.png "Optional title")
![数据流](../_static/packtrav-encap-decap.gif "Optional title")

## application layer 应用层

- 为解决某一类应用问题而生的，每一个服务需要用不同的协议，规定应用进程在通信时所遵循的协议
- 数据格式 `[HEAD(以太网标头) [HEAD(IP标头) [HEAD(TCP标头) DATA(应用层数据包)]]]`

### [HTTP](http)

### TELNET 远程登录协议

- connect to ports and query them for functionality
- 基于 TCP 连接将向主机发送文字命令
- 常用于登录路由器或高性能交换机等网络设备进行相应的设置
- telnet 命令 利用 TELNET 协议实现远程登录的客户端程序
- 服务端默认端口 23
- 客户端 通常与目标主机 23 号端口连接，并与监听这个端口的服务端程序 telnetd 进行交互
- 测试服务器指定端口是否可用
  - 通过客户端 telnet 命令模拟 HTTP 请求
  - 无需任何认证即可发送内容，容易造成通信窃听和非法侵入的危险

```sh
openssl s_client -starttls smtp \
-connect example.com:587

telnet 主机名(或IP) TCP端口号
telnet www.badu.com 80
```

### [SSH Secure Shell](ssh)

- SSH 本身是一种协议，有多种实现，最常见 OpenSSH
- 可以加密通信内容，是加密的远程登录协议，通过在网络中建立安全隧道来实现 SSH 客户端与服务器之间的连接，可以在不安全的网络中为网络服务提供安全的传输环境
- 服务器后台守护进程 sshd
- 客户端 SSH 远程连接，默认监听端口号是 22
- 过程
  - 远程主机收到用户的登录请求，把自己公钥发给用户
  - 用户使用这个公钥，将登录密码加密后，发送回来
  - 远程主机用自己私钥，解密登录密码，如果密码正确，就同意用户登录
- 威胁
  - 中间人攻击：攻击者插在用户与远程主机之间，用伪造的公钥，获取用户的登录密码，再用这个密码登录远程主机
    - 在通过 SSH 首次进行远程登录的时候，系统会要求你比对返回的公钥是否与目标服务器上的公钥信息一致，查看公钥 `ssh-keyscan -t ECDSA -p 22 laravelacademy.org`
- 每个用户都有自己 `known_hosts` 文件，此外还有一个系统级的 `/etc/ssh/ssh_known_hosts`文件，用于保存对所有用户都可信赖的远程主机的公钥
- 免密码登录远程服务器:`cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys`

### FTP File Transfer Protocol 文件传输协议

- 在两个相连计算机之间进行文件传输的协议
- 服务端守护进程 vsftpd
- 控制连接 一个 TCP 连接用于控制包含用户登录和验证、发送文件的名称、发送方式设置
  - 利用这个连接，可以通过 ASCII 码字符串发送请求和接收应答。但在这个连接上无法发送数据，只能通过另一个专门的 TCP 连接实现数据传输
  - 服务器以被动方式打开用于 FTP 的端口 21，客户端则主动发起连接。
  - 该连接将命令从客户端传给服务器，并传回服务器的应答。
  - 常用命令：list——获取文件目录；reter——取一个文件；store——存一个文件。
- 数据连接 
	- 进行文件 GET（RETR）、PUT（STOR）、以及文件预览（LIST）等操作时，每次都会建立一个用于数据传输的 TCP 连接。
	- 数据传输完毕后，传输数据连接被断开，然后在控制用的连接上继续进行命令或应答的处理
	- 数据传输端口 20
- 站在 FTP 服务器的角度,有两种工作模式
	- 主动模式 PORT
		- 客户端随机打开一个大于 1024 的端口 N，向服务器的命令端口 21 发起连接，同时开放 N+1 端口监听，并向服务器发出 “port N+1” 命令，由服务器从自己的数据端口 20，主动连接到客户端指定的数据端口 N+1
	- 被动模式 PASV
		- 当开启一个 FTP 连接时，客户端打开两个任意的本地端口 N（大于 1024）和 N+1。
		- 第一个端口连接服务器的 21 端口，提交 PASV 命令。
		- 然后，服务器会开启一个任意的端口 P（大于 1024），返回“227 entering passive mode”消息，里面有 FTP 服务器开放的用来进行数据传输的端口。
		- 客户端收到消息取得端口号之后，会通过 N+1 号端口连接服务器的端口 P，然后在两个端口之间进行数据传输

```sh
yum install vsftpd -y

# 添加ftp帐号和目录 先检查一下nologin的位置，通常在/usr/sbin/nologin或者/sbin/nologin下。 使用下面的命令创建帐户，该命令指定了/www/wwwroot为用户pwftp的家目录，您可以自己定义帐户名和目录：
useradd -d /www/wwwroot -s /sbin/nologin pwftp
passwd pwftp
chown -R pwftp:pwftp /www/wwwroot
mkdir www
mkdir wwwroot

# /etc/vsftpd/vsftpd.conf 将配置文件中 “anonymous_enable=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
hroot_local_user=YES
# vi编辑/etc/shells，如果该文件里没有/usr/sbin/nologin或者/sbin/nologin（具体看当前系统配置）则追加进去
service vsftpd start

telnet 114.215.241.29 21
USER ftpuser   # 通过 USER 指令设置 FTP 用户名
331 Please specify the password.
PASS ********  # 通过 PASS 指令设置 FTP 用户密码
230 Login successful.   # 返回 230 表示认证成功

ftp username@hostname
```

#### SFTP

- stands for SSH File Transfer Protocol, or Secure File Transfer Protocol, is a separate protocol packaged with SSH that works in a similar way over a secure connection.
- SSH 提供的一个客户端应用程序，主要用来安全地访问 FTP。因为 FTP 是不加密协议，很不安全，sftp就相当于将 FTP 放入了 SSH
- 指令
  - ls [directory] 列出一个远程目录的内容。如果没有指定目标目录，则默认列出当前目录
  - cd directory：从当前目录改到指定目录
  - mkdir directory：创建一个远程目录
  - rmdir path：删除一个远程目录
  - put localfile [remotefile]：本地文件传输到远程主机
  - get remotefile [localfile]：远程文件传输到本地

```sh
sftp [-oPort=custom_port] sammy@your_server_ip_or_remote_hostname

help | ?

# Local
lls
lcd Desktop

## Transferring Files
get -[r | P] remoteFile localFile # 下载重新命名 r:递归 P：维护权限与时间
put localFile # 上传文件

df -h # remote
du -f --max-depth=[遍历文件夹的深度] [file/folder] # 读性好的查看文件空间
! df -h # local

get /etc/group
!less group # 参看本地文件
```

### SMTP Simple Mail Transfer Protocol 简单邮件传输协议

- 一种会直连电源的邮件服务器，发送端和接收端通过邮件服务器进行邮件的收发。接收端从邮件服务器接收邮件使用 POP3 或 IMAP 协议
- 完整电子邮件机制由三部分组成
- 邮箱地址 `用户名@邮件服务器域名`
  - DNS 中注册邮箱地址及其作为发送地址时对应的邮件服务器的域名，这些映射信息被称作 MX 记录，可以在域名解析里看到这个选项
- 数据格式
  - 已经扩展到 MIME（Multipurpose Internet Mail Extensions，多用途互联网邮件扩展类型），可以发送图片、动画、音频、视频、应用程序等各种形式的数据.首部和正文（数据）两个部分组成
  - 首部中的 Content-Type 用于指定正文的数据类型
  - MIME 首部和正文之间也是通过一个空行分隔，并且如果正文数据比较大的情况下，还可以通过指定数据类型为 multipart/mixed 将多个 MIME 消息组合为一个
- 发送协议
  - SMTP 是发送电子邮件的协议，使用的是 TCP 的 25 号端口。SMTP 建立 TCP 连接之后，就会在这个连接上进行控制和应答以及数据的发送，客户端以文本命令方式发送请求
  - 一个不利之处在于它支持的是发送端主机的行为，而不是根据接收端的请求进行发送的行为，因此无法解决用户一开机就能接收到邮件.为了解决这个问题，引入了 POP

### POP Post Office Protocol 邮局协议

- 一种用于接收电子邮件协议，现在用的是第三版 POP3
- 发送端的邮件根据 SMTP 协议将被转发给一直处于插电状态的 POP 服务器，客户端再根据 POP 协议从 POP 服务器接收对方放过来的邮件。在这个过程中，为了防止他人盗窃邮件内容，还要做用户验证
- 服务端监听端口是 110

### IMAP Internet Message Access Protocol 互联网邮件访问协议

- 接收电子邮件协议
- 与 POP 协议的区别在于：在 POP 中邮件由客户端管理，而在 IMAP 中邮件由服务器管理。因此，在使用 IMAP 时，可以不必从服务器下载所有邮件就可以阅读。因为 IMAP 是在服务器上处理 MIME 信息，所以可以实现一封邮件中有 10 个附件时只下载其中 7 个这样的功能，这在带宽较窄的线路上非常有用。而且 IMAP 在服务器上对「已读/未读」信息和邮件进行分类管理，因此，即使在不同的计算机上打开邮箱，也能保持同步，这样一来，人们就可以通过个人电脑、手机、公司电脑连接到 IMAP 服务器后接收邮件，并且同步状态
- 服务端监听端口一般是 143

### DNS Domain Name System 域名系统

- DNS is an application layer protocol that runs on top of UDP(most of the times).
- DNS servers usually listen on port number 53. When a client makes a DNS request, after filling the necessary application payload, it passes the payload to the kernel via sendto system call.
- The kernel picks a random port number(>1024) as source port number and puts 53 as destination port number and sends the packet to lower layers. When the kernel on server side receives the packet, it checks the port number and queues the packet to the application buffer of the DNS server process which makes a recvfrom system call and reads the packet.
- This process by the kernel is called multiplexing(combining packets from multiple applications to same lower layers) and demultiplexing(segregating packets from single lower layer to multiple applications). Multiplexing and Demultiplexing is done by the Transport layer.
- 域名解析|主机名解析 通过域名，得到对应IP地址过程
- 为其他应用层协议工作的应用层协议，提供域名解析服务
- 由分层 DNS 服务器实现的分布式数据库。运行在 UDP 上，使用 53 端口
- DNS 劫持 原来网页被放置到一个iframe里，并注入广告，地址后面是不是有后缀。低延迟说明全国各地（至少在省内或者附近，不会南方跨到北方）直接返回被劫持的IP
- 互联网上几乎一切活动都以 DNS 请求开始。DNS 是 Internet 的目录,ISP (Internet Service Provider) 以及在 Internet 上进行监听的其他任何人，都能够看到访问的站点以及使用的每个应用.一些 DNS 提供商会出售个人 Internet 活动相关数据，或是利用这些数据向您发送有针对性的广告
- 利用 DNS 实现负载均衡，并且在配置运营商CDN机房时也是重要的一部分。

```sh
sudo tcpdump -s 0 -A -i any port 53
```

#### 记录  record

- 域名与IP之间对应关系的
- Domain_name 适用于哪个域名
- TTl `Time_to_live`：表明记录生存周期，最多可以缓存该记录多长时间
  - 任何一条 DNS 缓存，在超过过期时间后都必须丢弃， 没超时的时候，DNS 缓存也可以被主动或者被动地刷新
- Class 一般总是IN
- Type 类型
  - A Address   域名指向的IPv4 地址
  - AAAA IPv6 地址
  - NS Name Server 返回保存下一级域名信息的服务器地址
	- 该记录只能设置为域名，不能设置为IP地址
	- 为了服务的安全可靠，至少应该有两条NS记录
	- 记录 DNS 域对应的权威服务器域名
  - MX Mail eXchange 返回接收电子邮件的服务器地址
	  - 邮件服务器的域名必须要有对应 A 记录
  - CNAME Canonical Name 规范名称
	  - 返回另一个域名，即当前查询的域名是另一个域名的跳转。
	  - 用于域名的内部跳转，为服务器配置提供灵活性，用户感知不到。
	  -为防止冲突 ,一旦设置CNAME记录以后，就不能再设置其他记录了（比如A记录和MX记录）
  - PTR Pointer Record 逆向查询 用于从IP地址查询域名
- Value 则value是一个IPv4地址
- nslookup query Internet name servers
- [ipaddress](https://www.ipaddress.com/)

```sh
# Display your DNS server and target IP address
nslookup google.com
```

#### DNS 服务器 DNS Server

- 因特网上存储域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串
- 如果大家都去同一个地方访问某一台服务器，时延将会非常大。因而，DNS 服务器，一定要设置成高可用、高并发和分布式的
- 任何 DNS 服务器都可以找到并访问根域 DNS 服务器,客户端只要能够找到任意一台 DNS 服务器，就可以找到根域 DNS 服务器，然后再一路顺藤摸瓜找到位于下层的某台目标 DNS 服务器
- 设计为分布式集群的工作方式：使用分布式层次数据库模式以及缓存方法来解决单点集中式的问题
- 用户量大，缓存了大量的 DNS 记录，有效地降低了上游 DNS 服务器的压力，也加快了网络上的 DNS 查询速度
- 域名中，越靠右的位置表示其层级越高
- 根域名服务器 Root DNS Server 保存所有顶级区域的权威域名服务器记录
  - 负责解析顶级域名，给出顶级域名 DNS 服务器地址
  - 全世界仅有十三组根域名服务器，从A.ROOT-SERVERS.NET一直到M.ROOT-SERVERS.NET，服务器 ip 地址基本不会变动
  - 域名是 “"，空字符串。全限定域名（FQDN） `.`，因为 FQDN 总是以`.` 结尾
- 顶级域名服务器 Top-level DNS Server TLDs  `.com .cn` 等国际、国家级域名
  - 由 ICANN（互联网名称与数字地址分配机构）负责管理
  - 给出权威 DNS 服务器的 IP 地址
  - 每个顶级域名都对应各自的服务器，之间完全独立的。.cn 的域名解析仅由 .cn 顶级域名服务器提供
  - 目前国际 DNS 系统中已有上千个 TLD，包括中文「.我爱你」甚至藏文域名，详细列表参见 IANA TLD 数据库
  - 除国际可用 TLD，还有一类类似「内网 IP 地址」的“私有 TLD”，最常见的比如 xxx.local xxx.lan，被广泛用在集群通信中
- 权威 DNS 服务器 Authoritative DNS Server
	- 返回相应主机的 IP 地址
- 次级域 Second Level Domains SLD 个人/企业能够买到的域名，比如 `baidu.com`
  - 每个次级域名都有一到多个权威 DNS 服务器，这些 DNS 服务器会以 NS 记录形式保存在对应的顶级域名（TLD）服务器中。
- 子域 Sub Domians|三级域名 `*.baidu.com` 统统都是 baidu.com 的子域
  - 每一个子域都可以有自己独立的权威 DNS 服务器，通过在子域中添加 NS 记录实现
  - 用户可以任意分配在自己域里面名称
- 本地 DNS 服务器 local DNS server
	- 每个 ISP(Internet Service Provider) 都有一台本地 DNS 服务器，起着代理作用，并将该请求转发到 DNS 服务器层次系统中
- [WHOIS ](https://whois.icann.org/en/lookup?name=bluebird89.cyou) 确定注册机构

#### 域名解析

- DNS Resolver 域名解析器
	- DHCP机制 动态的，每次上网时由网关分配
	- 手动配置 事先指定固定地址。Linux系统保存在/etc/resolv.conf文件
		- 减少每次查询
- 正向解析 将域名解析为 IP 地址
- 反向解析
  - 记录类型 PTR 记录，提供将 IP 地址反向解析为域名的功能
  - 因为域名是从右往左读的,最右侧是根 `www.baidu.com.`而 IP 的网段（如 192.168.0.0/16）刚好相反，是左边优先。 因此 PTR 记录的“域名”必须将 IP 地址反着写，末尾再加上 .in-addr.arpa. 表示这是一个反向解析的域名。（ipv6 使用 ip6.arpa.）
- 查询方式
  - 递归查询 Recursive query 如果主机所询问本地域名服务器不知道被查询域名 IP 地址，那么本地域名服务器就以 DNS 客户端身份，向其他根域名服务器继续发出查询请求报文，而不是让该主机自己进行下一步的查询
  - 迭代查询 Iteration query 当根域名服务器收到本地域名服务器发出迭代查询请求报文时，要么给出所要查询的 IP 地址，要么告诉本地域名服务器：下一步应当向哪一个域名服务器进行查询。然后让本地域名服务器进行后续的查询，而不是替本地域名服务器进行后续的查询。
  - 客户端到 Local DNS 服务器，Local DNS 与上级 DNS 服务器之间属于递归查询；DNS 服务器与根 DNS 服务器之前属于迭代查询
- first looks at its cache 查询本地域名服务器
	- look up first in file (/etc/hosts)
	  - `C:\Windows\System32\drivers\etc\hosts`隐藏文件没有扩展名
	  - `/etc/hosts`
	- use DNS protocol to do the resolution if there is no match in /etc/hosts.
	- The linux system makes a DNS request to the first IP in /etc/resolv.conf. If there is no response, requests are sent to subsequent servers in resolv.conf. These servers in resolv.conf are called DNS resolvers. The DNS resolvers are populated by DHCP or statically configured by an administrator.
	- 通过 DHCP 配置，本地 DNS 由网络服务商（ISP），如电信、移动等自动分配，通常就在网络服务商的某个机房。
	- 本地域名服务器作为代理寻找IP
- 能找到就直接返回 IP 地址。如果没有，本地 DNS 会去问它的根域名服务器
- 寻找根域名服务器 The `.`is called root domain and those IPs are known to the DNS resolver software.   根域名`.root`对于所有域名都是一样的(简写 `.`)，所以平时是省略所有域名尾部
	- The DNS server breaks “`linkedin.com`” to `.`  `com.` and `linkedin.com.` and starts DNS resolution from `.`
- 顶级域名服务器 DNS resolver queries the root domain Nameservers to find the right nameservers which could respond regarding details for "com.". The address of the authoritative nameserver of “com.” is returned.
- 权威 DNS 服务器 Now the DNS resolution service contacts the authoritative nameserver for “com.” to fetch the authoritative nameserver for “linkedin.com”.
- Once an authoritative nameserver of “linkedin.com” is known, the resolver contacts Linkedin’s nameserver to provide the IP address of “linkedin.com”.
- 负载均衡 用域名代替IP
	- 内部负载均衡 对内服务
	- 全局负载均衡 GSLB，Global Server Load Balanc 对外服务
		- 通过配置 CNAME 的方式，给 object.yourcompany.com 起一个别名，例如 object.vip.yourcomany.com，然后告诉本地 DNS 服务器，让它请求 GSLB 解析这个域名，GSLB 就可以在解析这个域名的过程中，通过自己的策略实现负载均衡。通过区分运营商(配置不同运营商机房)、区域（同一运营商机房不同区域） 两层负债
		- 第一层 GSLB，通过查看请求它的本地 DNS 服务器所在的运营商，就知道用户所在的运营商。假设是移动，通过 CNAME 的方式，通过另一个别名 object.yd.yourcompany.com，告诉本地 DNS 服务器去请求第二层的 GSLB。
		- 第二层 GSLB，通过查看请求它的本地 DNS 服务器所在的地址，就知道用户所在的地理位置，然后将距离用户位置比较近的 Region 里面，六个内部负载均衡（SLB，Server Load Balancer）的地址，返回给本地 DNS 服务器。
	- gslb 失灵一般是因为一个ns请求gslb的时候，看不到用户真实的ip，从而不一定是最优的
- 内网解析
	- 内网的服务器都默认使用局域网 DNS 服务器进行解析。该解析器可以只解析自己的私有 DNS 域，而将其他 DNS 域的解析 forward 到公网 DNS 解析器去
	- 私有 dns 域也可使用公网不存在的 TLD
	- 会覆盖掉公网同名域(如果公网上有这个域的话)
- `dig` a userspace DNS system which creates and sends request to DNS resolvers and prints the response it receives to the console.显示整个查询过程
	- DNS 请求可以被抢答 `dig www.bennythink.com +short`

```sh
## `/etc/resolv.conf`
ns3.dnsowl.com # name silo default name server
ns3.dnsowl.com
ns3.dnsowl.com

host -a baidu.com  # host 基本就是 dig 的弱化版，不过 host 有个有点就是能打印出它测试过的所有 FQDN

nslookup baidu.com # 和 host 没啥大差别，多个交互式查询不过一般用不到
whois baidu.com # 查询域名注册信息，内网诊断用不到

dig linkedin.com
dig +trace linkedin.com
dig math.stackexchange.com

; <<>> DiG 9.10.6 <<>> math.stackexchange.com # 查询参数和统计
;; global options: +cmd
;; Got answer:

;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION: # 查询内容：域名的A记录
;math.stackexchange.com.        IN  A
;; ->>HEADER<< - opcode: QUERY, status: NOERROR, id: 14912

;; ANSWER SECTION: # 服务器答复:有四个A记录，即四个IP地址。600是TTL值（Time to live 的缩写），表示缓存时间，即600秒之内不用重新查询。
math.stackexchange.com. 300 IN  A   151.101.65.69
math.stackexchange.com. 300 IN  A   151.101.1.69
math.stackexchange.com. 300 IN  A   151.101.193.69
math.stackexchange.com. 300 IN  A   151.101.129.69

# NS记录（Name Server的缩写），即哪些服务器负责管理stackexchange.com的DNS记录。 四个域名服务器的IP地址，这是随着前一段一起返回的。
;; Query time: 119 msec
;; SERVER: 223.5.5.5#53(223.5.5.5) # 本机的DNS服务器是223.5.5.5，查询端口是53
;; WHEN: Sun Apr 08 23:54:53 CST 2018
;; MSG SIZE  rcvd: 104

dig @4.2.2.2 math.stackexchange.com # 显示向其他DNS服务器查询的结果

# 主机名.次级域名.顶级域名.根域名，即
host.sld.tld.root

dig +trace math.stackexchange.com
# 第一段列出根域名.的所有NS记录，即所有根域名服务器 根据内置的根域名服务器IP地址，DNS服务器向所有这些IP地址发出查询请求，询问math.stackexchange.com的顶级域名服务器com.的NS记录。最先回复的根域名服务器将被缓存，以后只向这台服务器发请求。
# 第二段显示.com域名的13条NS记录，同时返回的还有每一条记录对应的IP地址。 然后，DNS服务器向这些顶级域名服务器发出查询请求，询问math.stackexchange.com的次级域名stackexchange.com的NS记录
# 显示stackexchange.com有四条NS记录，同时返回的还有每一条NS记录对应的IP地址。 然后，DNS服务器向上面这四台NS服务器查询math.stackexchange.com的主机名
# 这四个IP地址都可以访问到网站。并且还显示，最先返回结果的NS服务器

# dig ns com
# dig ns stackexchange.com

dig +short ns stackexchange.com # 显示简化的结果
dig -x 192.30.252.153 # 查询PTR记录

# 可以查看指定的记录类型
dig a github.com
dig ns github.com
dig mx github.com

host github.com # host命令可以看作dig命令的简化版本。返回当前请求域名的各种记录
host 192.30.252.153
nslookup #  命令用于互动式地查询域名记录
whois github.com # 用来查看域名的注册情况

sudo killall -HUP mDNSResponder
sudo killall mDNSResponderHelper
sudo dscacheutil -flushcache

ifconfig /flushdns # 刷新DNS
```

```sh
# Google Public DNS IP addresses
8.8.8.8
8.8.4.4
2001:4860:4860::8888
2001:4860:4860::8844

# SDNS（`http://www.sdns.cn/`）
1.2.4.8
210.2.4.8

# OneDNS
112.124.47.27 # 南方首选/北方备用
114.215.126.16 # 北方首选/南方备用
42.236.82.22 # 共用

# Public DNS+
119.29.29.29
182.254.116.116

# 114
114.114.114.114
114.114.114.115
## 拦截钓鱼病毒木马网站，增强网银、证券、购物、游戏、隐私信息安全
114.114.114.119
114.114.115.119
## 学校或家长可选，拦截色情网站，保护少年儿童免受网络色情内容的毒害
114.114.114.110
114.114.115.110

# Cloudflare
1.1.1.1
1.0.0.1
2606:4700:4700::1111
2606:4700:4700::1001

# BaiduDNS
180.76.76.76
2400:da00::6666

# alidns
223.5.5.5
223.6.6.6
2400:3200::1
2400:3200:baba::1

# OpenDNS
208.67.222.222
208.67.220.220
2620:0:ccc::2
2620:0:ccd::2

# 台湾中华电讯的 DNS
168.95.192.1
168.95.192.2

# 香港宽频的 DNS：
203.80.96.9
203.80.96.10

# DNSPod DNS+
119.29.29.29
182.254.116.116

# Neustar UltraDNS IPv6
2610:a1:1018::1
2610:a1:1019::1
2610:a1:1018::5

## V2EX DNS
199.91.73.222 
178.79.131.110

# tsinghua
101.6.6.6
2001:da8:ff:305:20c:29ff:fe1f:a92a
# 清华大学 TUNA 协会 IPv6 DNS 服务器
2001:da8::666

# 中科大DNS
202.38.64.1
202.112.20.131
202.141.160.95
202.141.160.99

202.141.176.95
202.141.176.99

# 北京邮电大学 IPv6 DNS 服务器
2001:da8:202:10::36
2001:da8:202:10::37

# 上海交通大学 IPv6 DNS 服务器
2001:da8:8000:1:202:120:2:100
2001:da8:8000:1:202:120:2:101

# 中科院网络信息中心 IPv6 DNS 服务器
2001:cc0:2fff:1::6666

# 北京交通大学 IPv6 DNS 服务器
2001:da8:205:2060::188

# 北京科技大学 IPv6 DNS 服务器
2001:da8:208:10::6
# 科技网 IPv6 DNS 服务器
2001:cc0:2fff:2::6

# 下一代互联网北京研究中心
240C::6666
240C::6644

# CNNIC IPv6 DNS 服务器
1.2.4.8
210.2.4.8
2001:dc7:1000::1

# Quad9 DNS IBM 发起的 Quad9 提供的公共免费 DNS 上海
9.9.9.9
149.112.112.112
```

#### HTTPDNS

- 传统 DNS 问题
	- 传统基于 UDP 协议的公共 DNS 服务极易发生 DNS 劫持，从而造成安全问题
	- 缓存 本地域名解析服务
		- IP 缓存更新，无法访问或者使得全局负载均衡失败
		- 静态内容缓存 运营商把一些静态页面，缓存到本运营商的服务器内，用户请求的时候，就不用跨运营商进行访问，既加快了速度，也减少了运营商之间流量计算的成本。在域名解析的时候，不会将用户导向真正的网站，而是指向这个缓存的服务器。页面更新的时候就出问题了
	- 转发：判断错服务器来源
	- 出口 NAT：权威的 DNS 服务器，就没办法通过这个地址，来判断客户到底是来自哪个运营商，而且极有可能因为转换过后的地址，误判运营商，导致跨运营商的访问。
	- 域名更新 解析结果的 TTL 时间限制太长
	- 解析延迟
- 通过 HTTP 协议直接向权威 DNS 服务器发起请求，绕过运营商的 Local DNS、中间 DNS 递归解析器，代替传统基于 UDP 协议的 DNS 交互，有效防止了域名劫持，提高域名解析效率
- 缓存设计
	- 将解析速度和更新速度全部掌控在自己手中。
	- 一方面，解析的过程，不需要本地 DNS 服务递归的调用一大圈，一个 HTTP 的请求直接搞定，要实时更新的时候，马上就能起作用
	- 另一方面为了提高解析速度，本地也有缓存，缓存是在客户端 SDK 维护的，过期时间、更新时间，都可以自己控制。
- 同步机制
	- 同步进行
		- 优点 实时性好
		- 缺点 如果有多个请求都发现过期的时候，同时会请求 HttpDNS 多次，其实是一种浪费。
		- Cache-Aside 机制 先读缓存，不命中读数据库，同时将结果写入缓存。
	- 异步进行
		- 优点 可以将多个请求都发现过期的情况，合并为一个对于 HttpDNS 的请求任务，只执行一次，减少 HttpDNS 的压力。同时可以在即将过期的时候，就创建一个任务进行预加载，防止过期之后再刷新，称为预加载。
		- 缺点是当前请求拿到过期数据的时候，如果客户端允许使用过期数据，需要冒一次风险。如果过期的数据还能请求，就没问题；如果不能请求，则失败一次，等下次缓存更新后，再请求方能成功。
		- Refresh-Ahead 机制，即业务仅仅访问缓存，当过期的时候定期刷新。在著名的应用缓存 Guava Cache 中，有个 RefreshAfterWrite 机制，对于并发情况下，多个缓存访问不命中从而引发并发回源的情况，可以采取只有一个请求回源的模式。在应用架构的缓存中，也常常用数据预热或者预加载的机制。
- 调度设计
	- 由于客户端嵌入了 SDK，因而就不会因为本地 DNS 的各种缓存、转发、NAT，让权威 DNS 服务器误会客户端所在的位置和运营商，而可以拿到第一手资料。
	- 客户端的 SDK 会收集网络请求数据，如错误率、请求时间等网络请求质量数据，并发送到统计后台，进行分析、聚合，以此查看不同的 IP 的服务质量。
	- 服务端，应用可以通过调用 HttpDNS 的管理接口，配置不同服务质量的优先级、权重。HttpDNS 会根据这些策略综合地理位置和线路状况算出一个排序，优先访问当前那些优质的、时延低的 IP 地址。
- 解决问题
	- Local DNS 劫持：由于 HttpDns 通过 IP 直接请求 HTTP 获取服务器 A 记录地址，不存在向本地运营商询问 domain 解析过程，所以从根本避免了劫持问题。
	- 平均访问延迟下降：由于是 IP 直接访问省掉了一次 domain 解析过程，通过智能算法排序后找到最快节点进行访问。
	- 用户连接失败率下降：通过算法降低以往失败率过高的服务器排序，通过时间近期访问过的数据提高服务器排序，通过历史访问成功记录提高服务器排序。
	- 权威 DNS 服务器能直接获取到客户端的真实 IP（而不是某个中间 DNS 递归解析器的 IP），能实现就近调度。
	- 因为是直接与权威 DNS 服务器连接，避免了 DNS 缓存污染的问题
- 如何进行改造支持 HttpDns
	- 阿里云 HttpDNS 服务 `http://203.107.1.1/d?host=www.linkedkeeper.com`

#### 域名注册服务

- [NameSilo](https://www.namesilo.com/)
	- 域名注册
	- 二级域名解析配置
		- 登录后点击右上角  Manage My Domains
		- 已经购买的域名。然后点击右边的 蓝色小球 编辑 DNS
		- 点击上方的A，在 hostname 里填 www，ipv4 address 填服务器的ip，TTL改成 3600
  - 便宜域名生效慢
- [godaddy](https://www.godaddy.com/)

#### 解析服务

- Dnsmasq
	- 提供 DNS 缓存和 DHCP 服务功能。作为域名解析服务器(DNS)，dnsmasq可以通过缓存 DNS 请求来提高对访问过的网址的连接速度。作为DHCP 服务器，dnsmasq 可以用于为局域网电脑分配内网ip地址和提供路由。DNS和DHCP两个功能可以同时或分别单独实现。dnsmasq轻量且易配置，适用于个人用户或少于50台主机的网络。此外还自带了一个 PXE 服务器
	- 将 Dnsmasq 作为本地DNS服务器使用，直接修改电脑的本地DNS的IP地址即可
	- 应对ISP的DNS劫持（反DNS劫持），输入一个不存在的域名，正常的情况下浏览器是显示无法连接，DNS劫持会跳转到一个广告页面。先随便nslookup 一个不存在的域名，看看ISP商劫持的IP地址
	- 智能DNS加快解析速度，打开/etc/dnsmasq.conf文件，server=后面可以添加指定的DNS，例如国内外不同的网站使用不同的DNS
	- 配置 /etc/dnsmasq.conf
		- resolv-file 定义dnsmasq从哪里获取上游DNS服务器的地址， 默认从/etc/resolv.conf获取。
		- strict-order 表示严格按照resolv-file文件中的顺序从上到下进行DNS解析，直到第一个解析成功为止。
		- listen-address 定义dnsmasq监听的地址，默认是监控本机的所有网卡上。
		- address 启用泛域名解析，即自定义解析a记录，例如：address=/long.com/192.168.115.10 访问long.com时的所有域名都会被解析成192.168.115.10
		- bogus-nxdomain 对于任何被解析到此 IP 的域名，将响应 NXDOMAIN 使其解析失效，可以多次指定,通常用于对于访问不存在的域名，禁止其跳转到运营商的广告站点
		- server 指定使用哪个DNS服务器进行解析，对于不同的网站可以使用不同的域名对应解析。例如：server=/google.com/8.8.8.8#表示对于google的服务，使用谷歌的DNS解析
	- 解析流程
		- 先去解析 hosts 文件， 再去解析/etc/dnsmasq.d/下的*.conf文件，并且这些文件的优先级要高于dnsmasq.conf
		- 自定义的resolv.dnsmasq.conf中的DNS也被称为上游DNS，这是最后去查询解析的
		- 不想用hosts文件做解析:在 /etc/dnsmasq.conf 中加入no-hosts
	- dnsmasq dnscrypt 加上国内外分流
	- [dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list):Chinese-specific configuration to improve your favorite DNS server. Best partner for chnroutes.
- [ChinaDNS](https://github.com/shadowsocks/ChinaDNS):Protect yourself against DNS poisoning in China.
- [dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy):dnscrypt-proxy 2 - A flexible DNS proxy, with support for encrypted DNS protocols. <https://dnscrypt.info>
- [tenta-dns](https://github.com/tenta-browser/tenta-dns):Recursive and authoritative DNS server in go, including DNSSEC and DNS-over-TLS <https://tenta.com/test>
- [Cloudflare](https://www.cloudflare.com):域名注册服务,解析加速
- onedns   117.50.10.10    52.80.52.52纯净版
- [DNSpod](https://console.dnspod.cn/)
- [NextDNS](https://nextdns.io/):Block ads, trackers and malicious websites on all your devices. Get in-depth analytics about your Internet traffic. Protect your privacy and bypass censorship. Shield your kids from adult content.
- [hosts](https://github.com/googlehosts/hosts) 镜像 <https://coding.net/u/scaffrey/p/hosts/git>
- [hosts](https://github.com/racaljk/hosts)

```sh
# NetworkManager (manage /etc/resolv.conf)
127.0.0.1:53 dnsmasq (dns cache)
127.0.0.1:53000 dnscrypt-proxy (user space DNS over HTTPS)

###  dnsmasq (system space) listen the :53 will read /etc/dnsmasq.conf
add server=127.0.0.1#53000 to set dnscrypt as upstream dns server
```

#### DNS 缓存污染 DNS cache pollution|DNS Spoofing

- 不是域名IP被墙。域名仍能被解析到正确的IP地址，只是客户端（指用户浏览器/服务请求端）不能与网站服务器握手，或通过技术阻断或干扰的方式阻止握手成功，以至达到超时、屏蔽、连接重置、服务中断的现象
- 对所有经过防火长城（英语：Great Firewall，常用简称：GFW）的在UDP的53端口上的域名查询进行IDS入侵检测，一经发现与黑名单关键词相匹配的域名查询请求，会马上伪装成目标域名的解析服务器返回虚假的查询结果。由于通常的域名查询没有任何认证机制，而且域名查询通常基于无连接不可靠的UDP协议，查询者只能接受最先到达的格式正确结果，并丢弃之后的结果
  - 对于不了解相关知识的网民来说，由于系统默认从使用的ISP所提供的域名查询服务器去查询国外的权威服务器时，即被防火长城污染，进而使其缓存受到污染，因此默认情况下查询ISP的服务器就会获得虚假IP地址；而用户直接查询境外域名查询服务器（比如 Google Public DNS）时有可能会直接被防火长城污染，从而在没有任何防范机制的情况下仍然不能获得目标网站正确的IP地址。[1]
  - 因为TCP连接的机制可靠，防火长城理论上未对TCP协议下的域名查询进行污染，故现在能透过强制使用TCP协议查询真实的IP地址。而现实的情况是，防火长城对于真实的IP地址也可能会采取其它的手段进行封锁，或者对查询行为使用TCP重置攻击的方法进行拦截，故能否真正访问可能还需要其它翻墙的手段。
  - 通常情况下无论使用设置在中国大陆的DNS服务还是使用设置在海外的DNS服务，因为解析结果都需要穿过GFW，所以都会被GFW污染。但是仍有一些设置在中国大陆的小型DNS使用技术手段回避GFW的污染并提供不受污染的结果，通常使用这些小型DNS也能够访问其他被封锁的网站。
  - DNS污染的污染IP不是一成不变的，污染的无效IP在一段时间后会更新。
- [检测](https://www.checkgfw.com/)

#### [dnsperftest](https://github.com/cleanbrowsing/dnsperftest)

DNS Performance test

```sh
sudo apt-get install bc dnsutils

git clone --depth=1 https://github.com/cleanbrowsing/dnsperftest/
cd dnsperftest

bash ./dnstest.sh
bash ./dnstest.sh |sort -k 22 -n
```

### Dynamic Host Configuration Protocol DHCP 动态主机配置协议

- 配置一段共享 IP 地址。每一台新接入的机器都通过 DHCP 协议，来这个共享的 IP 地址里申请，然后自动配置好就可以
- 通过 DHCP 动态获取 IP 地址，大大省去配 IP 信息繁琐的过程
- DHCP 客户端进程监听 68 端口，DHCP 服务端进程监听 67 端口
- 工作方式
  - DHCP DISCOVER 客户端首先发起 DHCP 发现报文（DHCP DISCOVER）  IP 数据报，由于客户端没有 IP 地址，也不知道 DHCP 服务器的地址，所以使用的是 UDP 广播通信
    - 广播目的地址 255.255.255.255（端口 67）,源 IP 地址  0.0.0.0（端口 68）
    - UDP 封装了 BOOTP。其实 DHCP 是 BOOTP 的增强版，但是如果你去抓包的话，很可能看到的名称还是 BOOTP 协议。
    - DHCP 客户端将该 IP 数据报传递给链路层，链路层然后将帧广播到所有的网络中设备。
  - DHCP OFFER DHCP 服务端收到 DHCP 发现报文时，用 DHCP 提供报文（DHCP OFFER） 向客户端做出响应
    - MAC 地址唯一可以方便配置，重复则无法配置
    - 报文使用 广播地址 255.255.255.255 为目的地址，该报文信息携带服务器提供可租约的 IP 地址、子网掩码、默认网关、DNS 服务器以及 IP 地址租用期。
    - 为此客户保留为它提供的 IP 地址，从而不会为其他 DHCP 客户分配此 IP 地址。
  - DHCP REQUEST 客户端收到一个或多个服务器的 DHCP 提供报文后，从中选择一个服务器，并向选中的服务器发送 DHCP 请求报文（DHCP REQUEST）进行响应，回显配置的参数。
    - 一般是最先到达的那个，并且会向网络发送一个 DHCP Request 广播数据包，包中包含客户端的 MAC 地址、接受的租约中的 IP 地址、提供此租约的 DHCP 服务器地址等，并告诉所有 DHCP Server 它将接受哪一台服务器提供的 IP 地址，并请求撤销它们提供的 IP 地址，以便提供给下一个 IP 租用请求者。
    - 由于还没有得到 DHCP Server 的最后确认，客户端仍然使用 0.0.0.0 为源 IP 地址、255.255.255.255 为目标地址进行广播。在 BOOTP 里面，接受某个 DHCP Server 的分配的 IP。
  - DHCP ACK 服务端返回给客户一个 DHCP ACK 报文，表明已经接受客户机的选择，并将这一 IP 地址的合法租用信息和其他的配置信息都放入该广播包，发给客户机
  - 一旦客户端收到 DHCP ACK 后，需要广播一下，让大家都知道。客户端能够在租用期内使用 DHCP 服务器分配的 IP 地址
- 收回和续租
  - 租期过去 50% 的时候，直接向为其提供 IP 地址的 DHCP Server 发送 DHCP request 消息包：
  - 服务器如果同意继续租用，则用 DHCP ACK 报文进行应答，客户机接收到该服务器回应的 DHCP ACK 消息包，会根据包中所提供的新的租期以及其他已经更新的 TCP/IP 参数，更新自己的配置
  - 服务器如果不同意继续租用，则用 DHCP NACK 报文，客户端就要停止使用租约的 IP 地址
- DHCP 交互中，全程使用 UDP 广播通信，如果 DHCP 服务器和客户端不是在同一个局域网内，出现 DHCP 中继代理
  - 对不同网段 IP 地址分配也可以由一个 DHCP 服务器统一进行管理
  - DHCP 客户端会向 DHCP 中继代理发送 DHCP 请求包，而 DHCP 中继代理在收到这个广播包以后，再以单播的形式发给 DHCP 服务器。
  - 服务器端收到该包以后再向 DHCP 中继代理返回应答，并由 DHCP 中继代理将此包转发给 DHCP 客户端

### [RTMP](../resource/video#RTMP)

### P2P peer-to-peer

- 无论是 HTTP 的方式，还是 FTP 的方式，都有一个比较大的缺点，难以解决单一服务器的带宽压力， 因为它们使用的都是传统的客户端服务器的方式
- 想要下载一个文件的时候，只要得到那些已经存在了文件的 peer，并和这些 peer 之间，建立点对点的连接，而不需要到中心服务器上，就可以就近下载文件。
- 一旦下载了文件，也就成为 peer 中的一员，旁边的那些机器，也可能会选择从你这里下载文件，所以使用 P2P 软件的时候，例如 BitTorrent，往往能够看到，既有下载流量，也有上传的流量，也即你自己也加入了这个 P2P 的网络，自己从别人那里下载，同时也提供给其他人下载。可以想象，这种方式，参与的人越多，下载速度越快，一切完美。
- 种子（.torrent）文件
	- announce（tracker URL）
	- 文件信息
		- info 区：该种子有几个文件、文件有多长、目录结构，以及目录和文件的名字
		- Name 字段：指定顶层目录名字
		- 每个段大小：BitTorrent（简称 BT）协议把一个文件分成很多个小段，然后分段下载
		- 段哈希值 将整个种子中，每个段的 SHA-1 哈希值拼在一起
- 下载
	- BT 客户端首先解析.torrent 文件，得到 tracker 地址
	- 连接 tracker 服务器。tracker 服务器回应下载者的请求，将其他下载者（包括发布者）的 IP 提供给下载者。
	- 下载者再连接其他下载者，根据.torrent 文件，两者分别对方告知自己已经有的块，然后交换对方没有的数据。
	- 此时不需要其他服务器参与，并分散了单个线路上的数据流量，因此减轻了服务器的负担。
	- 下载者每得到一个块，需要算出下载块的 Hash 验证码，并与.torrent 文件中的对比。如果一样，则说明块正确，不一样则需要重新下载这个块。这种规定是为了解决下载内容的准确性问题。
- 这种方式特别依赖 tracker。tracker 需要收集下载者信息的服务器，并将此信息提供给其他下载者，使下载者们相互连接起来，传输数据。虽然下载的过程是非中心化的，但是加入这个 P2P 网络的时候，都需要借助 tracker 中心服务器，这个服务器是用来登记有哪些用户在请求哪些资源。
- 弊端，一旦 tracker 服务器出现故障或者线路遭到屏蔽，BT 工具就无法正常工作了。

### Kademlia 协议

- DHT（Distributed Hash Table）的去中心化网络。每个加入这个 DHT 网络的人，都要负责存储这个网络里的资源信息和其他成员的联系信息，相当于所有人一起构成了一个庞大的分布式存储数据库。
	- 在 DHT 网络里面，每一个 DHT node 都有一个 ID。节点 ID 是一个随机选择的 160bits（20 字节）空间，文件的哈希也使用这样的 160bits 空间。
	- 每个 DHT node 都有责任掌握一些知识，也就是文件索引，也即它应该知道某些文件是保存在哪些节点上。只需要有这些知识就可以了，而它自己本身不一定就是保存这个文件的节点。
	- 每个 DHT node 不会有全局的知识，也即不知道所有的文件保存在哪里，它只需要知道一部分,用哈希算法计算出来
		- 每个文件可以计算出一个哈希值，而 DHT node 的 ID 是和哈希值相同长度的串
		- DHT 算法是这样规定的：如果一个文件计算出一个哈希值，则和这个哈希值一样的那个 DHT node，就有责任知道从哪里下载这个文件，即便它自己没保存这个文件。
		- 除了一模一样的那个 DHT node 应该知道，ID 和这个哈希值非常接近的 N 个 DHT node 也应该知道。什么叫和哈希值接近呢？例如只修改了最后一位，就很接近；修改了倒数 2 位，也不远；修改了倒数 3 位，也可以接受。总之，凑齐了规定的 N 这个数就行。
		- ID 相似 距离是通过异或（XOR）计算的
			- 01010 与 01000 距离，就是两个 ID 之间的异或值，为 00010，即为 2.高位不同的，表示距离更远一些；低位不同的，表示距离更近一些，总的距离为所有的不同的位的距离之和。
			- 在 Kademlia 网络中，位置近不算近，ID 近才算近
- 任何一个 BitTorrent 启动之后，都有两个角色
	- 一个是 peer，监听一个 TCP 端口，用来上传和下载文件，这个角色表明，这里有某个文件
	- 另一个角色 DHT node，监听一个 UDP 的端口，通过这个角色，节点加入一个 DHT 的网络。
- 新的节点 node new 上线了。如果想下载文件 ，首先要加入 DHT 网络
	- 在这种模式下，种子.torrent 文件里面就不再是 tracker 的地址了，而是一个 list 的 node 的地址，而所有这些 node 都是已经在 DHT 网络里面的。当然随着时间的推移，很可能有退出的，有下线的，但是我们假设，不会所有的都联系不上，总有一个能联系上。
	- node new 只要在种子里面找到一个 DHT node，就加入了网络。
	- node new 会计算文件的哈希值，并根据这个哈希值了解到，和这个哈希值匹配，或者很接近的 node 上知道如何下载这个文件
	-  node new 不知道怎么联系上 可以下载 的 node，因为种子里面的 node 列表里面很可能没有 node ，但是可以问，DHT 网络特别像一个社交网络，node new 只有去它能联系上的 node 问
	-  在 DHT 网络中，每个 node 都保存一定的联系方式，但是肯定没有 node 的所有联系方式。如果找不到 Node，也能找到和 Node 的 ID 很像的节点
	-  DHT 网络中，节点之间通过互相通信，也会交流联系方式，也会删除联系方式。
	-  在 node C 上，告诉 node new，下载文件 1，要去 B、D、 F，于是 node new 选择和 node B 进行 peer 连接，开始下载，它一旦开始下载，自己本地也有文件 1 了，于是 node new 告诉 node C 以及和 node C 的 ID 很像的那些节点，我也有文件 1 了，可以加入那个文件拥有者列表了。
	-  node new 上没有文件索引，但是根据哈希算法，一定会有某些文件的哈希值是和 node new 的 ID 匹配上的。在 DHT 网络中，会有节点告诉它，既然加入了咱们这个网络，也有责任知道某些文件的下载地址。
-  DHT 网络 node 关系维护
	-  Node 关系节点 按距离分层 ID 为 01010
	-  只有最后 1 位不同 01011，与基础节点的异或值为 00001，即距离为 1，节点归为“k-bucket 1”
	-  从倒数第 2 位开始不同，即 01000 和 01001，与基础节点异或值为 00010 和 00011，即距离范围为 2 和 3；对于 01010 而言，这样的节点归为“k-bucket 2”
	-  如果一个节点的 ID，前面所有位数相同，从倒数第 i 位开始不同，这样的节点只有 2^(i-1) 个，与基础节点的距离范围为`[2^(i-1), 2^i)`；对于 01010 而言，这样的节点归为“k-bucket i”
	-  差距越大，陌生人越多，但是不能都放下，所以每一层都只放 K 个，这是参数可以配置
-  查找
	-  node A 的 ID 为 00110，要找 node B ID 为 10000，异或距离为 10110，距离范围在`[2^4, 2^5)`，这个目标节点可能在“k-bucket 5”中，这就说明 B 的 ID 与 A 的 ID 从第 5 位开始不同，所以 B 可能在“k-bucket 5”中。
	-  A 看看自己的 k-bucket 5 有没有 B。如果有，太好了，找到了；
	-  如果没有，在 k-bucket 5 里随便找一个 C。因为是二进制，C、B 都和 A 的第 5 位不同，那么 C 的 ID 第 5 位肯定与 B 相同，即它与 B 的距离会小于 2^4，相当于比 A、B 之间的距离缩短了一半以上。
	-  查询机制，是通过折半查找的方式来收缩范围，对于总的节点数目为 N，最多只需要查询 log2(N) 次，就能够找到
-  节点沟通指令
	-  PING：测试一个节点是否在线，还活着没，相当于打个电话，看还能打通不。
	-  STORE：要求一个节点存储一份数据，既然加入了组织，有义务保存一份数据。
	-  FIND_NODE：根据节点 ID 查找一个节点，就是给一个 160 位的 ID，通过上面朋友圈的方式找到那个节点。
	-  FIND_VALUE：根据 KEY 查找一个数据，实则上跟 FIND_NODE 非常类似。KEY 就是文件对应的 160 位的 ID，就是要找到保存了文件的节点。
-  更新关系节点数据
	-  每个 bucket 里的节点，都按最后一次接触的时间倒序排列，这就相当于，最近联系过的人往往是最熟的。
	-  每次执行四个指令中的任意一个都会触发更新。
	-  当一个节点与自己接触时，检查它是否已经在 k-bucket 中，也就是说是否已经在。
	-  如果在，那么将它挪到 k-bucket 列表的最底，也就是最新的位置，刚联系过，就置顶一下，方便以后多联系；
	-  如果不在，新的联系人要不要加到通讯录里面呢？假设通讯录已满的情况，PING 一下列表最上面，也即最旧的一个节点。
	-  如果 PING 通了，将旧节点挪到列表最底，并丢弃新节点，老朋友还是留一下；
	-  如果 PING 不通，删除旧节点，并将新节点加入列表，这人联系不上了，删了吧。

## session layer 会话层

## Presentation Layer 表示层

## transport layer 传输层

- 端到端传输数据的基本功能.在原有的上层的数据外围标记两个标签：第一源端口，第二目的端口，从这个端口出去，访问另一个端口  数据 段（Segments）
- 面向进程：使用端口号识别在传输层上一层的应用层中所要进行处理的具体程序
- 众多协议大多以客户端/服务端的形式运行,作为服务端的程序有必要提前启动，准备接收客户端的请求
  - 这些服务端程序在 UNIX 系统中叫守护进程
- 协议实现通常包含在操作系统自带的网络模块中

```sh
  10.10.27.115 # ip
  255.255.255.0 # 子网掩码
  10.10.27.0 # 网络
  0.0.0.115 # 主机地址

  arp -a
```

### Socket

- SOCK_DGRAM 类型
  - 只有一个接收缓冲区，而不存在发送缓冲区。数据的发送是直接进行的，而不管对端是否能够正常接收，也不管对端接收缓冲区是否充满。
  - 由于UDP是没有流量控制的，发送端可以很容易地就淹没接收者（更慢），导致接收方UDP丢弃数据报。
  - UDP报文并不保证顺序，所以接收缓冲区里的报文需要手动排序（如有必要）
  - UDP并不需要手动拆包——面向数据报的报文，并不会在缓冲区中自动合并
- TCP socket
  - 内核中都有一个发送缓冲区和一个接收缓冲区——TCP的全双工工作模式以及TCP的滑动窗口就是依赖这两个独立的buufer以及buffer的填充状态。
  - 对端发送过来数据，内核会存入接收缓冲区。缓冲区数据会一直保留直到应用层 read() 取走数据，在此过程中，TCP/IP协议栈继续执行，不断的将新的报文数据填充到接收缓冲区后面，直到填满为止。
  - 接下来发生的动作：通知对端TCP协议中的窗口关闭。这个便是滑动窗口的实现，用以保证TCP套接口接收缓冲区不会溢出，从而保证了TCP是可靠传输。因为对方不允许发出超过所通告窗口大小的数据。 这就是TCP的流量控制，如果对方无视窗口大小而发出了超过窗口大小的数据，则接收方TCP将丢弃它。
- 最大连接数
  - 通过 ulimit 配置文件描述符的数目
  - 内存
- C10K：一台机器要维护 1 万个连接，就要创建 1 万个进程或者线程，那么操作系统是无法承受的

#### 多进程

- 创建子进程使用 fork 函数。在父进程的基础上完全拷贝一个子进程。
- 在 Linux 内核中，会复制文件描述符的列表，也会复制内存空间，还会复制一条记录当前执行到了哪一行程序的进程。
- 复制完毕之后，父进程和子进程都会记录当前刚刚执行完 fork。这两个进程刚复制完的时候，几乎一模一样，只是根据 fork 的返回值来区分到底是父进程，还是子进程。
- 如果返回值是 0，则是子进程；如果返回值是其他的整数，就是父进程。
- 因而父进程刚才因为 accept 创建的已连接 Socket 也是一个文件描述符，同样也会被子进程获得。子进程就可以通过这个已连接 Socket 和客户端进行互通了，当通信完毕之后，就可以退出进程，
- 那父进程如何知道子进程干完了项目，fork 返回的时候，如果是整数就是父进程,这个整数就是子进程的 ID，父进程可以通过这个 ID 查看子进程是否完成项目，是否需要退出。

![进程复制过程](../_static/fork_datastructure.jpg)

#### 多线程

- 通过 pthread_create 创建一个线程，也是调用 do_fork。不同的是，虽然新的线程在 task 列表会新创建一项，但是很多资源，例如文件描述符列表、进程空间，还是共享的，只不过多了一个引用而已
- 新的线程也可以通过已连接 Socket 处理请求，从而达到并发处理的目的。

![进程生成过程](../_static/proccess_datastructure.png)

#### IO 多路复用

- 一个线程维护多个 Socket，所有的Socket 都放在一个文件描述符集合 fd_set 中
- 调用 select 函数来监听文件描述符集合是否有变化
  - 一旦有变化，就会依次查看每个文件描述符。
  - 发生变化的文件描述符在 fd_set 对应的位都设为 1，表示 Socket 可读或者可写，从而可以进行读写操作
  - 然后再调用 select，接着盯着下一轮的变化。
  - 同时盯的 Socket 数量由 FD_SETSIZE 限制
- 函数 epoll 在内核中实现不是通过轮询方式，而是通过注册 callback 函数方式，当某个文件描述符发送变化的时候，就会主动通知
  - epoll_create 创建一个 epoll 对象，也是一个文件，也对应一个文件描述符，同样也对应着打开文件列表中的一项。在这项里面有一个红黑树，在红黑树里，要保存这个 epoll 要监听的所有 Socket。
  - 当 epoll_ctl 添加一个 Socket 的时候，其实是加入这个红黑树，同时红黑树里面的节点指向一个结构，将这个结构挂在被监听的 Socket 的事件列表中。
  - 当一个 Socket 来了一个事件的时候，可以从这个列表中得到 epoll 对象，并调用 call back 通知它。这种通知方式使得监听的 Socket 数据增加的时候，效率不会大幅度降低，能够同时监听的 Socket 的数目也非常的多了
  - 上限就为系统定义的、进程打开的最大文件描述符个数。因而，epoll 被称为解决 C10K 问题的利器。

#### [ss socket statistics](https://www.cyberciti.biz/files/ss.html)

- 属于工具集 iproute2 替代 netstat
- 显示大量的套接字信息，包括使用的TCP流控算法，每个TCP会话的往返时间以及计算出的带宽和两个对等体之间的实际传输速率等，可以很好的用于网络监测和优化
- FILTER-NAME-HERE can be any one of the following,
	- all : All of the above states
	- established
	- syn-sent
	- syn-recv
	- fin-wait-1
	- fin-wait-2
	- time-wait
	- closed
	- close-wait
	- last-ack
	- listen
	- closing
	- connected : All the states except for listen and closed
	- synchronized : All the connected states except for syn-sent
	- bucket : Show states, which are maintained as minisockets, i.e. time-wait and syn-recv.
	- big : Opposite to bucket state.

```sh
ss -s # Print a summary of socket status
ss -l # Show all listening sockets

# ## Display All tcp|udp|raw|unix Sockets
ss -t|u|w|x -a 

#  All Established SMTP|http Connections
ss -o state established '( dport = :ssh or sport = :ssh )'

ss -ant | awk '{print $NF}' | grep -v '[a-z]' | sort | uniq -c # List the number and type of active network connections

# Find all local processes connected to X server.
ss -x src /tmp/.X11-unix/* 

# Lists all listening ports together with the PID of the associated process The PID will only be printed if you’re holding a root equivalent ID.
ss -tlnp 

# List all the TCP sockets in state -FIN-WAIT-1 for our httpd to network 202.54.1/24 and look at their timers:
ss -o state fin-wait-1 '( sport = :http or sport = :https )' dst 202.54.1/24

## tcp ipv4 ##
ss -4 state FILTER-NAME-HERE
 
## tcp ipv6 ##
ss -6 state FILTER-NAME-HERE

# Find out connection made by remote 123.1.2.100:http to our local virtual servers
# ss dst ADDRESS_PATTERN
ss dst 192.168.1.5:smtp
ss dst 192.168.1.5:443

# find out all ips connected to 75.126.153.214
ss src 75.126.153.214:smtp
ss src 75.126.153.214:25
```

#### netstat network status

- analyze interface, port, protocol statistics, and routing tables
- 一个网络信息统计工具。可以得到网卡接口上全部数据，路由表信息，网卡接口信息,列出系统上所有的网络套接字连接情况，包括 tcp, udp 以及 unix 套接字，另外还能列出处于监听状态（即等待接入请求）的套接字
- 参数
  - --listening -l List ports in listening mode
    - --all -a List all ports
    - --route -r Display routing tables
    - -t 列出 TCP 协议连接
    - -u 列出 UDP 协议连接
    - --interfaces -i Display TX/RX packet statistics for each interface
    - -n 禁用域名解析功能. 默认情况下 netstat 会通过反向域名解析技术查找每个 IP 地址对应的主机名,降低查找速度。如果觉没有必要知道主机名

```sh
# 列出所有连接
netstat -a

# 只列出TCP|UDP
time netstat -at|au

# 列出监听中连接
netstat -tnl

# 获取进程名、进程号以及用户 ID
nestat  -nlpt
netstat -tulpn

# 打印统计信息
netstat -s

# netstat持续输出
netstat -ct

# 打印active状态连接
netstat -atnp | grep ESTA

# 查看服务是否运行(npt)
netstat -aple| grep ntp

netstat -an | grep 3306
netstat -tunlp |grep 端口号 # 查看指定的端口号的进程情况 -t 显示tcp -u udp -n:拒绝显示别名，能数字数字 -l 列出在listen 服务状态 -p 显示相关程序名
lsof -i:80 # -i参数表示网络链接，:80指明端口号

ip netns exec

netstat -anlp|grep 80|grep tcp|awk '{print $5}'|awk -F: '{print $1}'|sort|uniq -c|sort -nr|head -n20 # 查看连接服务器 top10 用户端的 IP 地址
netstat -nat | awk  '{print  $5}' | awk -F ':' '{print $1}' | sort | uniq -c | sort -rn | head -n 10
netstat -nat |awk ‘{print $6}’|sort|uniq -c|sort -rn
ping api.jpush.cn | awk ‘{ print $0”    “ strftime(“%Y-%m-%d %H:%M:%S”,systime()) } ‘ >> /tmp/jiguang.log &

wget ftp://ftp.is.co.za/mirror/ftp.rpmforge.net/redhat/el6/en/x86_64/dag/RPMS/multitail-5.2.9-1.el6.rf.x86_64.rpm
yum -y localinstall multitail-5.2.9-1.el6.rf.x86_64.rpm
multitail -e "Accepted" /var/log/secure -l "ping baidu.com"

ps -aux | sort -rnk 3 | head -20
ps -aux | sort -rnk 4 | head -20

cat .bash_history | sort | uniq -c | sort -rn | head -n 10 (or cat .zhistory | sort | uniq -c | sort -rn | head -n 10 # 查看一下最常用的10个命令

# 输出nginx日志的ip和每个ip的pv，pv最高的前10
#2019-06-26T10:01:57+08:00|nginx001.server.ops.pro.dc|100.116.222.80|10.31.150.232:41021|0.014|0.011|0.000|200|200|273|-|/visit|sign=91CD1988CE8B313B8A0454A4BBE930DF|-|-|http|POST|112.4.238.213
awk -F"|" '{print $3}' access.log | sort | uniq -c | sort -nk1 -r | head -n10
```

#### [Tcpdump](http://www.tcpdump.org/)

- 类似工具在windows中 wireshark
- 命令行中通过指定表达式输出匹配捕获到的数据包的信息
- 采用底层库winpcap/libpcap实现，bpf过滤机制
- Packet structure
  - The TCP flags are in `tcp[13]` 
    - ACK = 0×10,
    - RST = 0×04
    - SYN = 0×02
    - FIN = 0×01
  - The ICMP type is in`  icmp[0] `
    - 0 (echo response)
    - 3 (destination unreachable)
    - 8 (echo request)
    - 11 (time exceeded)
  - IPv6
    - The transport layer protocol number is in the `ip6[6]` (“next header”) field
      - ICMP = 0×01
      - TCP = 0×06
      - UDP = 0×11
    - The IPv6 header is 40 bytes, assuming no extension headers, so `tcp[13]` maps to`  ip6[53] ` and `icmp[0]` maps to `ip6[40]`
- Recipes
  - Rejected : Capture RST and ICMP Destination Unreachable packets, useful when debugging a firewall to see what it rejects:`((tcp[13] & 4 == 4 ) || (ip6[6] == 6 && ip6[53] & 4 == 4 ) || (icmp[0] == 3) | | (icmp6 && ip6[40] == 1 ))`
  - Successful TCP handshakes Capture SYN+ACK packets to monitor successful TCP handshakes: `((tcp[13] & 0x12 = = 0x12 ) || (ip6[6] == 6 && ip6[53]&0x12 == 0x12 ))`
  - TCP termination Capture FIN+ACK packets to monitor TCP session terminations:`((tcp[13] & 0x11 == 0x11 ) || (ip6[6] == 6 && ip6[53] & 0x11 == 0x11 ))`
  - IPv6 neighbor and router discovery Capture ICMP6 neighbor solicitation / advertisement packets (135, 136) and ICMP6 router solicitation / advertisement / redirect packets (133, 134, 137): `(icmp6 && (ip6[40] >= 133 && ip6[40] <= 137))`
- 参数
  - -a 将网络地址和广播地址转变成名字
  - -A 打印ascii
  - -c 在收到指定包的数目后，tcpdump就会停止 Only get x number of packets and then stop.
  - -d 将匹配信息包的代码以人们能够理解的汇编格式给出
  - -D Show the list of available interfaces
  - -dd 将匹配信息包的代码以c语言程序段的格式给出
  - -ddd 将匹配信息包的代码以十进制的形式给出
  - -e 在输出行打印出数据链路层的头部信息 Get the ethernet header as well.
  - -E Decrypt IPSEC traffic by providing an encryption key.
  - -f 将外部的Internet地址以数字的形式打印出来
  - -F 从指定的文件中读取表达式,忽略其它的表达式
  - `-i eth0` 指定网卡
    - -i any get all interfaces
  - -l 使标准输出变为缓冲行形式 Line-readable output (for viewing as you save, or sending to other commands)
  - -n 不解析域名
  - -nn 表示端口也是数字，否则解析成服务名,不解析IP地址和端口的名称
  - -q Show less protocol information.
  - -r 从指定的文件中读取包(这些包一般通过-w选项产生)
  - -s 设置抓包长度，0表示不限制 Define the snaplength (size) of the capture in bytes. Use -s0 to get everything, unless you are intentionally capturing less.
  - -S Print absolute sequence numbers.
  - -t 在输出的每一行不打印时间戳 Give human-readable timestamp output.
  - -tttt Give maximally human-readable timestamp output.
  - -T 将监听到的包直接解释为指定的类型的报文，常见的类型有rpc（远程过程调用）和snmp（简单网络管理协议）
  - -v 输出一个稍微详细的信息，例如在ip包中可以包括ttl和服务类型的信息
  - -vv 输出详细的报文信息
  - -w 将抓取的包写入到某个文件中
  - -X 打印hex码 Show the packet’s contents in both hex and ascii.
  - -XX Same as -X, but also shows the ethernet header.
- Combinations
  - 非  `!`   not
  - 且  `&&`  and
  - 或  `||`  or
- 参考
  - [](https://hackertarget.com/tcpdump-examples/)

```sh
# networking tool which displays the TCP/IP packets transmitted and received by your system
tcpdump -c 15
tcpdump --help

# 网络过滤
tcpdump net 1.2.3.0/24
# 协议过滤
tcpdump -nn icmp

tcpdump -nn host 192.168.1.100
tcpdump -nn port 80


# find traffic by ip tcpdump host|src｜dst 1.1.1.1`
tcpdump ip6
tcpdump dst 192.168.0.2 and src net and not icmp
tcpdump 'src 10.0.2.4 and (dst port 3389 or 22)'
# verbose output, with no resolution of hostnames or port numbers, using absolute sequence numbers, and showing human-readable timestamps
tcpdump -ttnnvvS
tcpdump -nnvvS src 10.5.2.3 and dst port 3389

tcpdump -nvX src net 192.168.0.0/16 and dst net 10.0.0.0/8 or 172.16.0.0/16

# 端口过滤
tcpdump portrange 21-23
# based on packet size
tcpdump less 32
tcpdump greater 64
tcpdump <= 128

# reading / writing captures to a file (pcap)
tcpdump port 80 -w capture_file
tcpdump -r capture_file

# 抓取所有经过网卡1，目的或源地址IP为172.16.7.206的网络数据
tcpdump -i eth1 [src|dst] host 172.16.7.206
# 抓取所有经过网卡1，目的或源端口为1234的网络数据
tcpdump -i eth1 [src|dst] port 1234
tcpdump -i eth0 host 10.10.1.1

tcpdump -i eth1 [src|dst] net 192.168
# 抓取所有经过网卡1，协议类型为UDP的网络数据
tcpdump -i eth1 udp|arp|ip|tcp|icmp
# 抓取本地环路数据包
tcpdump -i lo udp # 抓取UDP数据
tcpdump -i lo udp port 1234 # 抓取端口1234的UDP数据
tcpdump -i lo port 1234 # 抓取端口1234的数据


# 抓取所有经过网卡1的SYN类型数据包
tcpdump -i eth1 ‘tcp[tcpflags] = tcp-syn’
# 抓取经过网卡1的所有DNS数据包（默认端口）
tcpdump -i eth1 udp dst port 53

# 逻辑语句过滤：抓取所有经过网卡1，目的网络是172.16，但目的主机不是192.168.1.200的TCP数据
tcpdump -i eth1 ‘((tcp) and ((dst net 172.16) and (not dst host 192.168.1.200)))’
# 抓取所有经过 eth1，目标 MAC 地址是 00:01:02:03:04:05 的 ICMP 数据
tcpdump -i eth1 '((icmp) and ((ether dst host 00:01:02:03:04:05)))'
# 抓取所有经过网卡1，目的主机为172.16.7.206的端口80的网络数据并存储
tcpdump -i eth1 host 172.16.7.206 and port 80 -w /tmp/xxx.cap

# 只抓 SYN 包
tcpdump -i eth1 'tcp[tcpflags] = tcp-syn'
# 抓 SYN, ACK
tcpdump -i eth1 'tcp[tcpflags] & tcp-syn != 0 and tcp[tcpflags] & tcp-ack != 0'

# Isolate TCP RST flags.
tcpdump 'tcp[13] & 4!=0'
tcpdump 'tcp[tcpflags] == tcp-rst'

# Isolate TCP SYN flags.
tcpdump 'tcp[13] & 2!=0'
tcpdump 'tcp[tcpflags] == tcp-syn'

# Isolate packets that have both the SYN and ACK flags set.
tcpdump 'tcp[13]=18'

# Isolate TCP URG flags.
tcpdump 'tcp[13] & 32!=0'
tcpdump 'tcp[tcpflags] == tcp-urg'

# Isolate TCP ACK flags.
tcpdump 'tcp[13] & 16!=0'
tcpdump 'tcp[tcpflags] == tcp-ack'

# Isolate TCP PSH flags.
tcpdump 'tcp[13] & 8!=0'
tcpdump 'tcp[tcpflags] == tcp-push'

# Isolate TCP FIN flags.
tcpdump 'tcp[13] & 1!=0'
tcpdump 'tcp[tcpflags] == tcp-fin'

# both syn and rst set
tcpdump 'tcp[13] = 6'

# find http user agents
tcpdump -vvAls0 | grep 'User-Agent:'

# cleartext get requests
tcpdump -vvAls0 | grep 'GET'

# find http cookies
tcpdump -vvAls0 | grep 'Set-Cookie|Host:|Cookie:'

# find dns traffic
tcpdump -vvAs0 port 53

# find ftp traffic
tcpdump -vvAs0 port ftp or ftp-data

# find ntp traffic
tcpdump -vvAs0 port 123

# 抓 SMTP 数据
# 抓取数据区开始为"MAIL"的包，"MAIL"的十六进制为 0x4d41494c。
tcpdump -i eth1 '((port 25) and (tcp[(tcp[12]>>2):4] = 0x4d41494c))'

# 抓取所有经过1234端口的UDP网络数据
tcpdump udp port 1234

# 抓 HTTP GET 数据
tcpdump -i eth1 'tcp[(tcp[12]>>2):4] = 0x47455420' # "GET "的十六进制是 47455420
#抓 SSH 返回
tcpdump -i eth1 'tcp[(tcp[12]>>2):4] = 0x5353482D' # "SSH-"的十六进制是 0x5353482D

# 抓老版本的 SSH 返回信息，如"SSH-1.99.."
tcpdump -i eth1 '(tcp[(tcp[12]>>2):4] = 0x5353482D) and (tcp[((tcp[12]>>2)+4):2]= 0x312E)'
# 抓取端口号8000的GET包，然后写入GET.log
tcpdump -i eth0 '((port 8000) and (tcp[(tcp[12]>>2):4]=0x47455420))' -nnAl -w /tmp/GET.log

# 抓 DNS 请求数据
tcpdump -i eth1 udp dst port 53

# 抓取系统中的get,post请求（非https)
tcpdump -s 0 -v -n -l | egrep -i "POST /|GET /|Host:"

tcpdump -i any tcp and host 192.168.33.10 and port 80 -w http.pcap
tcpdump -i eth0 tcp and host 192.168.33.10 and port 80 -w tcp.sys_timeout.pcap
# 捕获特定网口数据包
tcpdump -i eth0
# 捕获特定个数(1000)的包
tcpdump -c 1000 -i eth0
# 将捕获的包保存到文件
tcpdump -w a.pcap -i eth0
# 读取pcap格式的包
tcpdump -r a.pcap
# 增加捕获包的时间戳
tcpdump -n -ttt -i eth0
# 指定捕获包的协议类型
tcpdump -i eth0 arp
# 捕获指定端口
tcpdump -i eth0 post 22
# 捕获特定目标ip+port的包
tcpdump -i eth0 dst address and port 22
# 捕获DNS请求和响应
tcpdump -i eth0 -s0 port 53
# 匹配Http请求头
tcpdump -s 0 -v -n -l | egrep -i "POST /|GET /|Host:"

# find ssh connections This one works regardless of what port the connection comes in on, because it’s getting the banner response.
tcpdump 'tcp[(tcp[12]>>2):4] = 0x5353482D'

# find cleartext passwords
tcpdump port http or port ftp or port smtp or port imap or port pop3 or port telnet -lA | egrep -i -B5 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|passwd= |password=|pass:|user:|username:|password:|login:|pass |user '

# find traffic with evil bit There’s a bit in the IP header that never gets set by legitimate applications, which we call the “Evil Bit”. Here’s a fun filter to find packets where it’s been toggled.
tcpdump 'ip[6] & 128 != 0'
```

#### socat(socket cat) "netcat++" (extended design, new implementation)

- 给 socat 提供两个地址，socat 干的活就是把两个地址的流对接起来。左边地址的输出传给右边，同时又把右边地址的输出传给左边，也就是一个双向的数据管道
- 地址类型
  - -/stdio，TCP, TCP-LISTEN, UDP, UDP-LISTEN, OPEN, EXEC, SOCKS, PROXY 等等
- 可用于端口监听、链接，文件和进程读写，代理桥接等等

```sh
sudo apt| yum install socat
# macOS
brew install socat

# 检测远程端口的可连接
# -d[ddd] 增加日志详细程度，-dd  Prints fatal, error, warning, and notice messages.
socat -dd - TCP:192.168.1.252:3306

# -v 显示详细信息
# -z 不发送数据，效果为立即关闭连接，快速得出结果
nc -vz 192.168.1.2 8080

# -vv 显示更详细的内容
# -w2 超时时间设为 2 秒
# 使用 nc 做简单的端口扫描
nc -vv -w2 -z 192.168.1.2 20-500

## 测试本机端口是否能正常被外部访问（检测防火墙、路由）
# 在本机监听一个 TCP 端口，接收到的内容传到 stdout，同时将 stdin 的输入传给客户端：
# 服务端启动命令，socat/nc 二选一
socat TCP-LISTEN:7000 -
# -l --listening
nc -l 7000
# 客户端连接命令，socat/nc 二选一
socat TCP:192.168.31.123:7000 -
nc 192.168.11.123 7000

### UDP 协议的测试也非常类似，使用 netcat 的示例如下：
# 服务端，只监听 ipv4
nc -u -l 8080
# 客户端
nc -u 192.168.31.123 8080
# 客户端本机测试，注意 localhost 会被优先解析为 ipv6! 这会导致服务端(ipv4)的 nc 接收不到数据！
nc -u localhost 8080

# 使用 socat 的 UDP 测试示例如下：
socat UDP-LISTEN:7000 -
socat UDP:192.168.31.123:7000 -

## 调试 TLS 协议
# 模拟一个 mTLS 服务器，监听 4433 端口，接收到的数据同样输出到 stdout：
# socat 需要使用同时包含证书和私钥的 pem 文件，生成方法如下
cat server.key server.crt > server.pem
cat client.key client.crt > client.pem

# 服务端启动命令
socat openssl-listen:4433,reuseaddr,cert=server.pem,cafile=client.crt -

# 客户端连接命令
socat - openssl-connect:192.168.31.123:4433,cert=client.pem,cafile=server.crt
# 或者使用 curl 连接(我们知道 ca.crt 和 server.crt 都能被用做 cacert/cafile)
curl -v --cacert ca.crt --cert client.crt --key client.key --tls-max 1.2 https://192.168.31.123:4433

# 上面的命令使用了 mTLS 双向认证的协议，可通过设定 verify=0 来关掉客户端认证

# socat 需要使用同时包含证书和私钥的 pem 文件，生成方法如下
cat server.key server.crt > server.pem

# 服务端启动命令
socat openssl-listen:4433,reuseaddr,cert=server.pem,verify=0 -

# 客户端连接命令，如果 ip/域名不受证书保护，就也需要添加 verify=0
socat - openssl-connect:192.168.31.123:4433,cafile=server.crt
# 或者使用 curl 连接，证书无效请添加 -k 跳过证书验证
curl -v --cacert server.crt https://192.168.31.123:4433

### 数据传输
# 以将 demo.tar.gz 从主机 A 发送到主机 B 为例,在数据发送方 A 执行
# -u 表示数据只从左边的地址单向传输给右边（socat 默认是一个双向管道）
# -U 和 -u 相反，数据只从右边单向传输给左边
socat -u open:demo.tar.gz tcp-listen:2000,reuseaddr
# 在数据接收方 B 执行如下命令，就能把文件接收到
socat -u tcp:192.168.1.252:2000 open:demo.tar.gz,create
# 如果觉得太繁琐，也可以直接通过 stdout 重定向
socat -u tcp:192.168.1.252:2000 - > demo.tar.gz

# 用 netcat 也可以实现数据传输
# 先在接收方启动服务端
nc -l -p 8080 > demo.tar.gz
# 再在发送方启动客户端发送数据
nc 192.168.1.2 8080 < demo.tar.gz

# 担当临时的 web 服务器
# 将监听 8080 端口，并将数据流和 web.py 的 stdio 连接起来，可以直接使用浏览器访问 http://<ip>:8080 来查看效果
socat TCP-LISTEN:8080,reuseaddr,fork SYSTEM:"python3 web.py"

##  端口转发
# 监听 8080 端口，建立该端口与 baidu.com:80 之间的双向管道
socat TCP-LISTEN:8080,fork,reuseaddr  TCP:baidu.com:80

# 注意指定 Host
curl -v -H 'Host: baidu.com' localhost:8080
```

### Transmission Control Protocol TCP 传输控制协议

- 提供面向连接的数据流支持、可靠性、流量控制、多路复用等服务

- TCP 在通信双方之间建立起一条基于字节流的全双工通道

- TCP 负责将数据分割并装入 IP 包，然后在到达的时候重新组合
  - 通过 IP 网络的面向连接的协议。使用握手建立和断开连接。发送的所有数据包保证以原始顺序到达目的地，用以下措施保证数据包不被损坏
  - 为了确保高吞吐量，Web 服务器可以保持大量的 TCP 连接，从而导致高内存使用。在 Web 服务器线程间拥有大量开放连接可能开销巨大，消耗资源过多，一个 memcached 服务器。连接池可以帮助除了在适用的情况下切换到 UDP。

- 对于需要高可靠性但时间不紧迫的应用程序很有用
  - SMTP
  - TELNET
  - HTTP
  - FTP

- 以下情况使用 TCP 代替 UDP
  - 需要数据完好无损
  - 想对网络吞吐量自动进行最佳评估

- 面向有连接的协议，只有在确认通信对端存在时才会发送数据
  - 顺序控制
    - 确认应答处理、重发控制以及重复控制等功能都可以通过序列号实现，序列号是按顺序给发送数据的每一个字节都标上号码的编号

- 基于连接的协议、端到端和可靠数据包发送

- 当应用程序希望通过 TCP 与另一个应用程序通信时，会发送一个通信请求。这个请求必须被送到一个确切的地址。在双方“握手”之后，TCP 将在两个应用程序之间建立一个全双工 (full-duplex) 的通信。在数据传送前分割为 IP 包，在到达时重组

- 建立在不可靠的网络层 IP 协议之上，IP协议并不能提供任何可靠性机制，TCP 可靠性完全由自己实现，提供的服务包括数据流传送、可靠性、有效流控、全双工操作和多路复用

- 特点
  - 提供一种面向连接的、可靠的字节流服务
  - 一个 TCP 连接中，仅有两方进行彼此通信。广播和多播不能用于 TCP
  - 使用校验和，确认和重传机制来保证可靠传输,甄别有害的数据包
  - 给数据分节进行排序，并使用累积确认保证数据的顺序不变和非重复
  - 使用滑动窗口机制来实现流量控制，通过动态改变窗口的大小进行拥塞控制
  - 能够确保连接的建立和数据包的发送

- 虽然是面向字节流的，但TCP传送的数据单元却是报文段。一个TCP报文段分为首部和数据两部分，而TCP的全部功能体现在它首部中的各字段的作用

- 四元组可以确定唯一一个连接:源端口和目的端口字段 socket（IP+端口号）。TCP的包是没有IP地址的，那是IP层上的事。但是有源端口和目标端口
  - 本地端口由16位组成,因此本地端口的最多数量为 2^16 = 65535个,本地的最大HTTP连接数为： 本地最大端口数65535 * 本地ip数1 = 65535 个
  - 远端端口由16位组成,因此远端端口的最多数量为 2^16 = 65535个,远端的最大HTTP连接数为：远端最大端口数65535 * 远端(客户端)ip数+∞ = 无限制
  - 源地址和目的地址的字段（32位）是在 IP 头部中，作用是通过 IP 协议发送报文给对方主机
  - 源端口和目的端口的字段（16位）是在 TCP 头部中，作用是告诉 TCP 协议应该把报文发给哪个进程

- 面向字节流：应用程序和TCP的交互是一次一个数据块（大小不等），但TCP把应用程序看成是一连串的无结构的字节流。TCP有一个缓冲，当应用程序传送的数据块太长，TCP就可以把它划分短一些再传送
  - 在连接持续的过程中，socket中收到的数据都是由同一台主机发出的，因此，只要保证数据是有序到达就行了，至于每次读取多少数据自己看着办。

#### 编程步骤

- 服务器端函数 socket() 创建一个**监听 Socket**
- 函数 setsockopt() 设置 socket 属性（可选）
- 函数 bind() 绑定IP地址、端口等信息到socket上
- 函数 listen() 开启监听
- 函数accept() 接收客户端连接
- 客户端函数connect() 连接服务器,参数中指明要连接的 IP 地址和端口号
- 发起三次握手。内核会给客户端分配一个临时端口。一旦握手成功，服务端的 accept 就会返回另一个 **已连接 Socket**
  - Socket 就是一个文件流，在 Linux 中就是以文件的形式存在的。还存在文件描述符。写入和读出，也是通过文件描述符
  - 每一个进程都有一个数据结构 task_struct，里面指向一个文件描述符数组，来列出这个进程打开的所有文件的文件描述符
  - 文件描述符是一个整数，是这个数组的下标
  - 数组中内容是一个指针，指向内核中所有打开文件的列表。既然是一个文件，就会有一个 inode，只不过 Socket 对应 inode 不像真正的文件系统一样，保存在硬盘上的，而是在内存中的。在这个 inode 中，指向 Socket 在内核中的 Socket 结构。
- 函数send()和recv()，或者read()和write()收发数据
- 客户端函数 close() 断开连接
- 关闭监听

![task_struct 结构](../_static/task_struct.png)

#### 数据结构维护

- TCP 协议栈中维护两个队列
  - 服务端收到客户端发起 SYN 请求，内核会把该连接存储到半连接队列，并向客户端响应 SYN+ACK
  - 客户端返回 ACK，服务端收到第三次握手 ACK，内核会把连接从半连接队列移除，然后创建新的完全的连接，并将其添加到 accept 队列，等待进程调用 accept 函数时把连接取出来
  - 不管是半连接队列还是全连接队列，都有最大长度限制，超过限制时，内核会直接丢弃，或返回 RST 包
- 半连接队列
  - 服务端收到请求未收到客户收到响应，
  - 查看 SYN_RECV 状态 `netstat -natp | grep SYN_RECV | wc -l`
  - 最大值不是单单由 max_syn_backlog 决定，还跟 somaxconn 和 backlog 有关系
  - 当 max_syn_backlog > min(somaxconn, backlog) 时， 半连接队列最大值 max_qlen_log = min(somaxconn, backlog) * 2;
  - 当 max_syn_backlog < min(somaxconn, backlog) 时， 半连接队列最大值 max_qlen_log = max_syn_backlog * 2;
  - max_qlen_log 是理论半连接队列最大值，并不一定代表服务端处于 SYN_REVC 状态的最大个数
  - 如果当前半连接队列的长度 「没有超过」理论半连接队列最大值  max_qlen_log，那么如果条件 3 成立，则依然会丢弃 SYN 包，也就会使得服务端处于 SYN_REVC 状态的最大个数不会是理论值 max_qlen_log

    - 服务端处于 SYN_RECV 状态的最大个数分为如下两种情况：
      - 如果「当前半连接队列」没超过「理论半连接队列最大值」，但是超过 max_syn_backlog - (max_syn_backlog >> 2)，那么处于 SYN_RECV 状态的最大个数就是 max_syn_backlog - (max_syn_backlog >> 2)；
      - 如果「当前半连接队列」超过「理论半连接队列最大值」，那么处于 SYN_RECV 状态的最大个数就是「理论半连接队列最大值」
- 开启 syncookies 功能 可以在不使用 SYN 半连接队列的情况下成功建立连接  `echo 1 > /proc/sys/net/ipv4/tcp_syncookies`
  - 0 关闭该功能
  - 1  仅当 SYN 半连接队列放不下时，再启用它
  - 2 无条件开启功能
  - 原理
    - 当服务器接受到 SYN 报文段时，不直接为该 TCP 分配资源，而只是打开一个半开的套接字
    - 使用 SYN 报文段的源Id，目的Id，端口号以及只有服务器自己知道的一个秘密函数生成一个 cookie，并把 cookie 作为序列号响应给客户端。
    - 如果客户端是正常建立连接，将会返回一个确认字段为 cookie + 1 的报文段
    - 接下来服务器会根据确认报文的源Id，目的Id，端口号以及秘密函数计算出一个结果，如果结果的值 + 1等于确认字段的值，则证明是刚刚请求连接的客户端，这时候才为该 TCP 分配资源
- 全连接队列 accept 队列
  - 使用 ss 查看 -l 显示正在监听的socket
    - `Recv-Q/Send-Q` 在「LISTEN 状态」和「非 LISTEN 状态」所表达的含义是不同的
    - 在「LISTEN 状态」时  `ss -lnt`
      - Recv-Q 当前全连接队列大小
      - Send-Q 当前全连接最大队列长度，上面的输出结果说明监听 8088 端口的 TCP 服务进程，最大全连接长度为 128
      - 客户端`wrk -t 6 -c 3000 -d 60s http://192.168.3.200:8080` 服务端 `ss -lnt| grep 8088`
      - 服务端执行多次 `ss -lnt` 发现当前 TCP 全连接队列上升到了 129 大小，超过最大 TCP 全连接队列,服务端则会丢掉后续进来的 TCP 连接
      - 如果 TCP 全连接队列过小，容易溢出。发生 TCP 全连接队溢出的时候，后续的请求就会被丢弃，这样就会出现服务端请求数量上不去的现象
        - 丢掉 TCP 连接个数统计 date;netstat -s | grep overflowed
        - 丢弃连接只是 Linux 的默认行为，还可以选择向客户端发送 RST 复位报文，告诉客户端连接已经建立失败. `cat /proc/sys/net/ipv4/tcp_abort_on_overflow`
          - 0 ：表示如果全连接队列满了，那么 server 扔掉 client  发过来的 ack ；
          - 1 ：表示如果全连接队列满了，那么 server 发送一个 reset 包给 client，表示废掉这个握手过程和这个连接
        - 要想知道客户端连接不上服务端，是不是服务端 TCP 全连接队列满的原因，那么可以把 tcp_abort_on_overflow 设置为 1，这时如果在客户端异常中可以看到很多 connection reset by peer 的错误，那么就可以证明是由于服务端 TCP 全连接队列溢出的问题
        - 通常情况下，应当把 tcp_abort_on_overflow 设置为 0，因为这样更有利于应对突发流量
          - 当 TCP 全连接队列满导致服务器丢掉了 ACK，与此同时，客户端的连接状态却是 ESTABLISHED，进程就在建立好的连接上发送请求。只要服务器没有为请求回复 ACK，请求就会被多次重发。如果服务器上的进程只是短暂的繁忙造成 accept 队列满，那么当 TCP 全连接队列有空位时，再次接收到的请求报文由于含有 ACK，仍然会触发服务器端成功建立连接。
          - 设为 0 可以提高连接建立的成功率，只有你非常肯定 TCP 全连接队列会长期溢出时，才能设置为 1 以尽快通知客户端
    - 在「非 LISTEN 状态」时  `ss -nt`
      - Recv-Q 已收到但未被应用进程读取的字节数
      - Send-Q 已发送但未收到确认的字节数
  - 最大值取决于 somaxconn 和 backlog 之间的最小值，也就是 min(somaxconn, backlog)
    - somaxconn 是 Linux 内核的参数，默认值是 128，可以通过 `/proc/sys/net/core/somaxconn` 来设置其值
    - backlog 是 listen(int sockfd, int backlog) 函数中的 backlog 大小，Nginx 默认值是 511，可以通过修改配置文件设置其长度
- 机制 `cat /proc/sys/net/ipv4/tcp_abort_on_overflow`
  - 两个队列,都有最大长度限制，超过限制时，内核会直接丢弃，或返回 RST 包

  - 0 表示如果全连接队列满了，server 扔掉 client  发过来的 ack,更有利于应对突发流量
    - 只要服务器没有为请求回复 ACK，请求就会被多次重发
    - 如果服务器上进程只是短暂的繁忙造成 accept 队列满，那么当 TCP 全连接队列有空位时，再次接收到的请求报文由于含有 ACK，仍然会触发服务器端成功建立连接

  - 1 表示如果全连接队列满了， server 发送一个 reset 包给 client，表示废掉这个握手过程和这个连接.
    - 客户端异常中可以看到很多 `connection reset by peer` 的错误，那么就可以证明是由于服务端 TCP .全连接队列溢出的问题.
    - 只有非常肯定 TCP 全连接队列会长期溢出时，才能设置为 1 以尽快通知客户端

  - 如果半连接队列满了，并且没有开启 tcp_syncookies，则会丢弃

  - 若全连接队列满了，且没有重传 SYN+ACK 包的连接请求多于 1 个，则会丢弃

  - 如果没有开启 `tcp_syncookies`，并且 max_syn_backlog 减去 当前半连接队列长度小于 (max_syn_backlog >> 2)，则会丢弃
- 如果已经建立连接，客户端突然出现故障了怎么办？
  - TCP设有一个保活计时器，客户端如果出现故障，服务器不能一直等下去
  - 服务器每收到一次客户端的请求后都会重新复位这个计时器，时间通常是设置为2小时，若两小时还没有收到客户端的任何数据，服务器就会发送一个探测报文段，以后每隔75秒发送一次。若一连发送10个探测报文仍然没反应，服务器就认为客户端出了故障，接着就关闭连接

#### 包头格式

- TCP 包中的序号字段表示该包中第一个字节的序号，序号位有4个字节，也即4G大小。

- TCP确认号表示希望对象下一次报文段的第一个字节的序号。

- TCP连接建立之后，所有的报文的ACK值都必须为1。

- TCP的PSH（push）值为1时，表示发送方需要立即发送该报文而不缓存，接收方需要立即将将该该报文交付给应用程序。

- TCP的SYN=1并ACK=0，表示发起连接请求，SYN=1并ACK=1表示接受连接请求，因此SYNC=1的包表示连接的请求或接收报文。

- TCP的窗口字段为2字节，窗口值告诉对方：从该报文确认号算起，接收方允许对方发送的字节数。之所以有这个窗口值，是因为接收方的缓存是有限的，因此需要进行流量控制。

- TCP的窗口值告诉对方：发送方的发送窗口不能超过接收方的接收窗口，TCP的窗口单位是字节，不是报文段。当接收方回复的窗口值为0时，发送方应立即停止发送，直到接收方重新发出一个新的窗口值为止。

- 前20个字节是固定的，后面有 4n 字节是根据需要而增加的选项（n是整数）。因此TCP首部的最小长度是20字节

- 源端口和目的端口 各2个字节

- 序列号 Sequence Number
  - 4个字节，TCP 连接中传送的字节流中的每个字节都按顺序编号，解决网络包乱序（reordering）问题。
  - 通过 SYN 包传给接收端主机，每发送一次数据，就累加一次该「数据字节数」的大小
  - 不会从0或1开始，而是在建立连接时由计算机生成的随机数作为初始值，通过 SYN 包发送给接收端主机
  - 建立连接和断开连接时虽然不传输数据，但也会作为一个字节增加对应的序列号

- 确认应答号 Acknowledgement Number
  - 4个字节，期望收到对方下一个报文的第一个数据字节的序号，用来解决不丢包的问题
  - 例如，B收到了A发送过来的报文，其序列号字段是501，而数据长度是200字节，这表明B正确的收到了A发送的到序号700为止的数据。因此，B期望收到A的下一个数据序号是701，于是B在发送给A的确认报文段中把确认号置为701

- 数据偏移 4位，TCP 所传输数据部分应该从 TCP 包的哪个位置开始计算，也可以将其看作 TCP 包的长度

- 保留 占6位，保留今后使用，目前应都位 0

- TCP Flag 状态位，用于操控TCP的状态机
  - CWR（Congestion Window Reduced）：与后面的ECE都是用于IP首部的ECN字段，为1时通知对方已将拥塞窗口缩小
  - ECE（ECN-Echo）：置为1时通知通信对方，从对方到这边的网络有拥堵
  - 紧急URG （Urgent Flag）当URG=1，表明紧急指针字段有效。告诉系统此报文段中有紧急数据
  - 确认ACK 仅当ACK=1时，确认号字段才有效。TCP规定，在连接建立后所有报文的传输都必须把 ACK 置1
  - 推送PSH (PuSH)：当两个应用进程进行交互式通信时，有时在一端的应用进程希望在键入一个命令后立即就能收到对方的响应，这时候就将PSH=1,接收  TCP  收到  PSH  =  1  的报文段，就尽快地交付接收应用进程，而不再等到整个缓存都填满了后再向上交付
  - 复位RST (ReSeT)：当RST=1，表明TCP连接中出现严重差错，必须释放连接，然后再重新建立连接
  - 同步SYN：在连接建立时用来同步序号。当SYN=1，ACK=0，表明是连接请求报文，若同意连接，则响应报文中应该使SYN=1，ACK=1
  - 终止FIN (Finish)：用来释放连接。当FIN=1，表明此报文的发送方的数据已经发送完毕，并且要求释放

- 窗口｜滑动窗口 Window｜Advertised-Window｜Sliding Window
  - 指通知接收方，发送本报文需要有多大的空间来接受。用于解决流控
  - 占 2 字节，用来让对方设置发送窗口的依据，单位为字节。窗口值 [0, 2^16-1]之间的整数,默认情况支持的最大窗口数是 65536字节/64KB
  - 指 TCP传输能接受的最大字节数，这个可以进行动态调节，也就是 TCP的滑动窗口，通过动态调整窗口大小，来控制发送数据速率
  - Ws: 窗口缩放调整因子
    - 为能够支持更多的缓冲数据 RFC 1323中就规定了 TCP 的扩展选项，其中窗口缩放调整因子就是其中之一
    - 这个参数是在 [SYN] 同步阶段进行协商的，结合抓包数据分析下。看到第一次请求协商的结果是 WS=256,然后再 ACK 阶段扩展因子生效，调整了窗口大小

- 检验和
  - 2 字节
  - 字段检验范围:首部和数据这两部分
  - 在计算检验和时，要在TCP 报文段的前面加上 12 字节的伪部(协议字段为6，表示TCP)

- 紧急指针
  - 占2字节，指出本报文段中的紧急数据的字节数
  - 指出在本报文段中紧急数据共有多少个字节(紧急数据放在本报文段数据的最前面)

- 选项：长度可变，定义一些其他可选参数
  - MSS Maxitum Segment Size 最大报文段长度 =TCP报文段长度-TCP首部长度
    - 指在TCP连接建立时，收发双发协商的通信时每一个报文段所能承载的数据字段的最大长度（并不是TCP报文段的最大长度，而是：MSS=TCP报文段长度-TCP首部长度），单位为字节（双方提供的MSS中的最小值，为本次连接的最大MSS值）（MSS选项只出现在SYN报文段中)
    - 这个值 TCP 协议在实现的时候往往用 MTU 值代替（减去 IP数据包包头大小 20Bytes和 TCP数据段的包头 20Bytes）,所以如果用链路层以太网(MTU  1500)，MSS值往往为1460。通讯双方会根据双方提供的MSS值得最小值确定为这次连接的最大MSS值。
    - Internet上标准 MTU（最小MTU，链路层网络为 x2.5 时）为576，如果不设置，则 MSS 默认值就为 536 个字节。很多时候，MSS值最好取512倍数
    - 分段与重组是在传输层完成
    - TCP 报文段长度大于MSS时，要进行分段
      - TCP 分段原因 MSS，IP 分片原因 MTU
      - 采用TCP协议进行数据传输是不会造成IP分片的，因为一旦TCP数据过大，超过了MSS，传输层就会对TCP包进行分段。 由于一直有MSS<=MTU，IP层对于TCP的分段数据就不用再分片了
  - 窗口扩大选项
  - 时间戳选项
  - 选择确认选项
  - Len 消息长度
    - 指数据报文段整个 TCP报文 = Header + packSize,所以这个消息长度就是指要传送的数据包总共长度，也就是 HTTP报文的大小

![TCP头格式](../_static/TCP-Header-01.jpg "TCP头格式")

#### TCP 状态机

- 状态编码：S指代服务器，C指代客户端，S&C表示两者，S/C表示两者之一
- LISTEN S等待从任意远程TCP端口的连接请求。侦听状态
- SYN-SENT C在发送连接请求后等待匹配的连接请求。通过connect()函数向服务器发出一个同步（SYNC）信号后进入此状态
- SYN-RECEIVED S已经收到并发送同步（SYNC）信号之后等待确认（ACK）请求
- ESTABLISHED S&C连接已经打开，收到的数据可以发送给用户。数据传输步骤的正常情况。此时连接两端是平等的
- FIN-WAIT-1 S&C主动关闭端调用close（）函数发出FIN请求包，表示本方的数据发送全部结束，等待TCP连接另一端的确认包或FIN请求包
- FIN-WAIT-2 S&C主动关闭端在FIN-WAIT-1状态下收到确认包，进入等待远程TCP的连接终止请求的半关闭状态。这时可以接收数据，但不再发送数据
- CLOSE-WAIT S&C被动关闭端接到FIN后，就发出ACK以回应FIN请求，并进入等待本地用户的连接终止请求的半关闭状态。这时可以发送数据，但不再接收数据
- CLOSING S&C在发出FIN后，又收到对方发来的FIN后，进入等待对方对连接终止（FIN）的确认（ACK）的状态
- LAST-ACK S&C被动关闭端全部数据发送完成之后，向主动关闭端发送FIN，进入等待确认包的状态
- TIME-WAIT S/C主动关闭端接收到FIN后，就发送ACK包，等待足够时间以确保被动关闭端收到了终止请求的确认包。按照RFC 793，一个连接可以在TIME-WAIT保证最大四分钟，即最大分段寿命（maximum segment lifetime）的2倍
- CLOSED S&C完全没有连接

![TCP协议状态机](../_static/tcpfsm.png)

#### 三次握手 Three-way Handshake

- 目的
  - 连接服务器指定端口，建立 TCP 连接
  - 同步连接双方的序列号和确认号,保证之后传输数据的顺序性.
  - 交换 TCP 窗口大小信息
- 同步序列编号 Synchronize Sequence Numbers SYN
  - 初始化 Sequence Number 初始值 TCP/IP 建立连接时使用的握手信号。在客户机和服务器之间建立 TCP 连接时，首先会发送的一个信号。
  - 客户端在接受到 SYN 消息时，就会在自己段内生成一个随机值 X，用来初始化和建立连接.起始序号是随着时间变化的，可以看成一个 32 位的计数器，每 4 微秒加一，如果计算一下，如果到重复，需要 4 个多小时，那个绕路的包早就死翘翘了，因为 IP 包头里面有个 TTL，也即生存时间。
  - 通信双方要互相通知对方自己初始化的 Sequence Number 作为以后数据通信序号，以保证应用层接收到数据不会因为网络上传输问题而乱序
  - RFC793 中认为 ISN 要和一个假的时钟绑定在一起ISN 每四微秒加一，当超过 2 的 32 次方之后又从 0 开始，要四个半小时左右发生 ISN 回绕
- 开始客户端和服务器都是处于 CLOSED 状态。服务器进程先创建传输控制块TCB，时刻准备接受客户进程连接请求，进入 LISTEN 状态
- 第一次握手 客户端发送同步报文，对齐
  - 客户进程创建传输控制块TCB，向服务器发出连接请求报文，同步位 SYN=1，序号 SEQ=x,进入SYN_SEND（同步已发送状态），等待服务器确认.
  - TCP规定：SYN报文段（SYN=1的报文段）不能携带数据，但需要消耗掉一个序号
- 第二次握手 SYN=1, seq=y, ack=x+1
  - 服务器收到请求报文后，同意连接，则发出确认报文，同步位SYN=1，ack  =x+1，序号 seq=y
  - 服务器进入 SYN_RECV （同步收到）状态。报文也不能携带数据，消耗一个序号
- 第三次握手(ACK=1，ack=y+1,seq =x+1)
  - 客户进程收到确认后，向服务器给出确认 ACK。确认报文 ack=y+1. TCP连接建立
  - 客户进程收到确认后，检查 ack 状态是否为 x+1，如果正确则将标志位 ACK 置为 1，ack=y+1，并将该数据包发送给 Server，Server 检查 ack 是否为 y+1，ACK 是否为 1，如果正确则连接建立成功
  - Client 和 Server 进入 ESTABLISHED 状态
  - TCP规定:ACK报文段可以携带数据，如果不携带数据则不消耗序号
  - 防止已经失效的连接请求报文突然又传送到了服务器，从而产生错误
- 为什么建立连接是三次握手
  - 防止已失效连接请求报文段突然又传送到服务端，因而产生错误
    - client 发出第一个连接请求报文段并没有丢失，而是在某个网络结点长时间滞留，以致延误到连接释放以后的某个时间才到达 server
    - 为保证服务端能收接受到客户端的信息并能做出正确的应答而进行前两次(第一次和第二次)握手
    - 为保证客户端能够接收到服务端的信息并能做出正确的应答而进行后两次(第二次和第三次)握手
- 理想状态下，TCP连接一旦建立，在通信双方中的任何一方主动关闭连接之前，TCP 连接都将被一直保持下去
- SACK_PERM
  - SACK 选项默认情况下，接受端接受到一个包后，发送 ACK 确认，但是，默认只支持顺序的确认，也就是说，发送 A, B, C 个包，如果收到了 A, C的包，B没有收到，那么对于 C，这个包是不会确认的，需要等 B这个包收到后再确认，那么 TCP 有超时重传机制，如果一个包很久没有确认，就会当它丢失了，进行重传，这样会造成很多多余的包重传，浪费传输空间
  - 为解决这个问题， SACK 提出选择性确认机制，启用 SACK 后，接受端会确认所有收到的包，这样发送端就只用重传真正丢失的包
- SYN 超时
  - server 端如果在一定时间内没有收到TCP会重发SYN-ACK
  - 在Linux下，默认重试次数为5次，重试间隔时间从 1s开始每次都翻售，5次的重试时间间隔为1s, 2s, 4s, 8s, 16s，总共31s，第5次发出后还要等32s都知道第5次也超时了
  - 总共需要 1s + 2s + 4s+ 8s+ 16s + 32s = 2^6 -1 = 63s，TCP才会把断开这个连接

#### 四次挥手 Four-way handshake

- TCP 全双工,发送方和接收方都需要Fin和Ack
- 数据传输完毕后，双方都可释放连接。最开始处于 ESTABLISHED 状态，然后一方主动关闭，另一方被动关闭
  - 在 socket 编程中，任何一方执行 close() 操作即可产生挥手操作，断开过程需要经过"四次挥手"（要对方关闭与对方关闭完成两次确认）,由TCP的半关闭（half-close）造成
- 第一次挥手(FIN=1，seq=x)
  - 主动关闭连接一方，调用 close(),kernel will send a FIN packet 发起一个断开请求（主动关闭”（active close）），进入 FIN-WAIT-1 状态
- 第二次挥手(ACK=1，ack=x+1)
  - 被动关闭一方收到 FIN 包后，发送一个确认包，表明自己接受到客户端关闭连接请求，但还没有准备好关闭连接,进入`CLOSE_WAIT`状态
  - 主动关闭一方等待对方关闭，则进入`FIN_WAIT_2`状态,等待被动关闭一方的应用程序调用close操作
  - Linux 有可以调整 tcp_fin_timeout 这个参数，设置一个超时时间,避免主动关闭一方一直等待
- 第三次挥手(FIN=1，seq=y)
  - 被动关闭一方在完成所有数据发送后，调用close()操作
  - 准备好关闭连接时，向客户端发送结束连接请求，FIN 为1，被动关闭一方进入LAST_ACK状态，等待对方 ACK
  - 在 RFC 2581中  4.2 节有提到ack可以延迟确认，只要求保证在 500ms 之内保证确认包到达即可。在这样的标准下，TCP确认是有可能进行合并延迟确认的
- 第四次挥手(ACK=1，ack=y+1)
  - 主动关闭一方收到FIN包，发送一个确认包，并进入 TIME_WAIT状态，等待可能出现的要求重传 ACK 包
  - 服务器端接收到确认包之后，关闭连接，进入 CLOSED 状态
  - 主动关闭一方等待 2MSL ( Maximum Segment Lifetime 最大报文段生存时间)时间，没有收到服务器端的 ack ，认为服务器端已经正常关闭连接，于是自己也关闭连接，结束TIME_WAIT->CLOSED状态 `netstat -a | grep TIME_WAIT | wc -l`
- 2MSL
  - 任何报文在网络上存在的最长时间，超过这个时间报文将被丢弃。因为 TCP 报文基于是 IP 协议的，而 IP 头中有一个 TTL 域，是 IP 数据报可以经过的最大路由数，每经过一个处理他的路由器此值就减 1，当此值为 0 则数据报将被丢弃，同时发送 ICMP 报文通知源主机。协议规定 MSL 为 2 分钟，实际应用中常用的是 30 秒，1 分钟和 2 分钟等。
  - 保证TCP协议全双工连接能够可靠关闭
  - 保证这次连接重复数据段从网络中消失
  - this socket can’t be reused for that time period to prevent any TCP state corruptions due to stray stale packets.
  - 怕最后一个 ACK包对方没收到，那么对方在超时后将重发第三次握手的FIN包，主动关闭端接到重发 FIN包后，可以再发一个ACK应答包
  - 在 TIME_WAIT 状态时，两端端口不能使用，要等到2MSL时间结束，才可继续使用
    - 当连接处于2MSL等待阶段时，任何迟到的报文段都将被丢弃
    - 有一个连接没有进入CLOSED状态之前，连接不能被重用的
- 关闭连接确是四次挥手呢？
  - 因为 TCP 是全双工协议，也就是说双方都要关闭，每一方都向对方发送 FIN 和回应 ACK
  - 当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到Server端所有的报文都发送完了，才能发送FIN报文，因此不能一起发送。故需要四步握手。
- 断开连接发起方在接受到接受方的 FIN 并回复 ACK 之后并没有直接进入 CLOSED 状态，而是进行了一波等待，等待时间为 2MSL
  - MSL 是 Maximum Segment Lifetime，即报文最长生存时间，RFC 793 定义的 MSL 时间是 2 分钟，Linux 实际实现是 30s，那么 2MSL 是一分钟。
  - 就是怕被动关闭方没有收到最后的 ACK，如果被动方由于网络原因没有到，那么它会再次发送 FIN，此时如果主动关闭方已经 CLOSED 那就傻了，因此等一会儿。
  - 假设立马断开连接，但是又重用了这个连接，就是五元组完全一致，并且序号还在合适的范围内，虽然概率很低但理论上也有可能，那么新的连接会被已关闭连接链路上的一些残留数据干扰，因此给予一定的时间来处理一些残留数据。
  - 问题
    - 如果服务器主动关闭大量的连接，那么会出现大量的资源占用，需要等到 2MSL 才会释放资源。
    - 如果是客户端主动关闭大量的连接，那么在 2MSL 里面那些端口都是被占用的，端口只有 65535 个，如果端口耗尽了就无法发起送的连接了
  - 解决
    - 快速回收，即不等 2MSL 就回收， Linux 的参数是 tcp_tw_recycle，还有 tcp_timestamps 不过默认是打开的
    - 重用，即开启 tcp_tw_reuse 当然也是需要 tcp_timestamps 的
- 关闭连接时，服务器收到对方的FIN报文时，仅仅表示对方不再发送数据了但是还能接收数据，而自己也未必全部数据都发送给对方了，所以己方可以立即关闭，也可以发送一些数据给对方后，再发送FIN报文给对方来表示同意现在关闭连接，因此，己方ACK和FIN一般都会分开发送，从而导致多了一次。

![TCP建/断链接](../_static/tcp_open_close.jpg)
![TCP状态转换图](../_static/tcp_status.jpg "Optional title")

```sh
netstat -napt

tcpdump -S -i any port 80
curl www.linkedin.com
```

#### 保证传输可靠性

- 数据包校验码
  - 目的 检测数据在传输过程中的任何变化
  - 若校验出包有错，则丢弃报文段并且不给出响应，这时TCP发送数据端超时后会重发数据
- 序列号保证有序
  - 报文段作为 IP数据报来传输，而IP数据报的到达可能会失序，因此TCP报文段到达可能会失序
  - 对失序数据根据序列号进行重新排序后交给应用层
- 连接管理 如果多次超时，连接就会断开

##### cumulative acknowledgment 累计应答

- 为保证不丢包，对于发送的包都要进行应答
- 这个应答也不是一个一个来的，而是会应答某个之前的 ID，表示都收到了
- ACK 600 确认应答报文丢失，也没关系，可以通话下一个确认应答进行确认，只要发送方收到 ACK 700 确认应答，就意味着 700 之前的所有数据「接收方」都收到了

##### 重发机制

- 通过肯定的确认应答（ACK）实现可靠的数据传输，当发送端将数据发出之后会等待对端的确认应答。如果确认应答，说明数据已经成功达到对端。反之，则数据有可能丢失。在一定时间内没有等到确认应答，发送端就认为数据已经丢失，并进行重发
- 超时重试
  - 发出一个段后，启动一个定时器，等待目的端确认收到这个报文段
  - 在一定时间内如果没有得到发送的数据报的ACK报文，那么就重新发送数据，直到发送成功为止
  - 时间不宜过短，时间必须大于往返时间 RTT，否则会引起不必要的重传。也不宜过长，这样超时时间变长，访问就变慢了。
  - 自适应重传算法（Adaptive Retransmission Algorithm） 估计往返时间，需要 TCP 通过采样 RTT 的时间，然后进行加权平均，算出一个值，而且这个值还是要不断变化的，因为网络状况不断地变化。除了采样 RTT，还要采样 RTT 的波动范围，计算出一个估计的超时时间。由于重传时间是不断变化的
  - 在 BSD Unix 和 Windows 中，超时都是按照 0.5 秒为单位进行控制，因此，重发超时都是 0.5 秒的整数倍。不过由于最初的数据包还不知道往返时间，因此其重发超时一般设置为 6 秒左右
  - 重发之后若还是收不到确认应答，则再次发送
  - 超时间隔加倍 每当遇到一次超时重传的时候，都会将下一次超时时间间隔设为先前值的两倍。两次超时，就说明网络环境差，不宜频繁反复发送。
  - 达到一定重发次数后，如果仍没有确认应答返回，就会判断为网络或对端主机发生异常，强制关闭连接。并且通知应用通信异常强行终止
- 快速重传 Fast Retransmit
  - 当接收方收到一个序号大于下一个所期望的报文段时，就会检测到数据流中的一个间隔，于是就会发送冗余 ACK，仍然 ACK 的是期望接收的报文段。
  - 当客户端收到三个冗余 ACK 后，就会在定时器过期之前，重传丢失报文段
  - 接收方发现 6 收到，8 也收到，但是 7 还没来，那肯定是丢了，发送 6 的 ACK，要求下一个是 7。接下来，收到后续包，仍然发送 6  ACK，要求下一个是 7。当客户端收到 3 个重复 ACK，就会发现 7 的确丢了，不等超时，马上重发
  - 重传的时候，是重传之前的一个，还是重传所有的问题
- Selective Acknowledgment SACK 选择性确认
  - 在 TCP 头部「选项」字段里加一个 SACK 的东西，可以将缓存的地图发送给发送方，发送方就可以知道哪些数据收到了，哪些数据没收到，知道了这些信息，就可以只重传丢失的数据。
  - 例如可以发送 ACK6、SACK8、SACK9，有了地图，发送方一下子就能看出来是 7 丢了
  - 必须双方都要支持。在 Linux 下，可以通过 net.ipv4.tcp_sack 参数打开这个功能（Linux 2.4 后默认打开）
- D-SACK　Duplicate SACK
  - 使用 SACK 来告诉发送方有哪些数据被重复接收了
  - 可以让发送方知道，是发出去的包丢了，还是接收方回应的 ACK 包丢了
  - 可以知道是不是「发送方」的数据包被网络延迟了
  - 可以知道网络中是不是把「发送方」的数据包给复制了
  - 通过 net.ipv4.tcp_dsack 参数开启/关闭这个功能（Linux 2.4 后默认打开）
- 丢弃重复数据：对于重复数据，能够丢弃重复数据

##### Flow Control 流量控制

- 一种让发送方根据接收方缓冲区所能接纳的数据能力控制发送的数据量机制
- 发送端根据自己实际情况发送数据，但接收端可能收到的是一个毫无关系的数据包又可能会在处理其它问题上耗费一些时间，甚至在高负荷的情况下无法接收任何数据。接收端将本该接收的数据丢弃的话，就又会触发重发机制，从而导致网络流量的无端浪费
- TCP 发送端和接收端都有缓存来保存这些记录
- 发送端缓存数据里按照包的 ID 一个个排列,根据处理的情况分成四个部分
  - 1 已发送并收到 ACK 确认的数据
  - 2 已发送但未收到 ACK 确认的数据
  - 3 未发送但总大小在接收方处理范围内（接收方还有空间）
  - 4 未发送但总大小超过接收方处理范围（接收方没有空间）
  - 用三个指针来跟踪在四个传输类别中的每一个类别中的字节
    - LastByteAcked 第一部分和第二部分的分界线，绝对指针 SND.UNA 指向已发送但未收到确认的第一个字节序列号，第二部分第一个字节
    - LastByteSent 第二部分和第三部分的分界线，绝对指针 SND.NXT 指向未发送但可发送范围的第一个字节的序列号，第三部分第一个字节
    - LastByteAcked + AdvertisedWindow（SND.WND） 第三部分和第四部分的分界线，指向第四部分第一个字节是个相对指针  SND.UNA + SND.WND 大小的偏移量
    - 相对指针（偏移）可用窗口大 = SND.WND -（SND.NXT - SND.UNA）
- 接收端的记录
  - 接受并且确认过的
  - 还没接收，但是马上就能接收
  - 还没接收，也没法接收
  - MaxRcvBuffer 最大缓存量
    - RCV.WND 表示接收窗口大小，会通告给发送方
  - 用两个指针进行划分
    - LastByteRead 之后是已经接收了，但是还没被应用层读取
    - NextByteExpected|RCV.NXT 一二部分分界线，第二部分第一个字节。指针指向期望从发送方发送来的下一个数据字节的序列号，
    - 二三部分分界线  LastByteRead + MaxRcvBuffer RCV.NXT + RCV.WND
  - `AdvertisedWindow=MaxRcvBuffer-((NextByteExpected-1)-LastByteRead)`
  - 接收端的窗口的起始点是下一个要接收并且 ACK 的包，即便后来的包都到了，放在缓存里面，窗口也不能右移，因为 TCP 的 ACK 机制是基于序列号的累计应答，一旦 ACK 了一个序列号，就说明前面的都到了，所以只要前面的没到，后面的到了也不能 ACK，就会导致后面的到了，也有可能超时重传，浪费带宽。
- 管理两个节点之间数据传输速率的过程，防止快速发送方致使慢速接收方缓冲区溢出。为接收机提供一种控制传输速度的机制，这样接收节点就不会被来自发送节点的数据淹没
- 滑动窗口 rwnd 是怕发送方把接收方缓存塞满，而拥塞窗口 cwnd，是怕把网络塞满

![半连接队列与全连接队列](../_static/commect_queue.png "Optional title")

###### 滑动窗口|可变窗口 rwnd

- 控制协议可变大小。让发送速率不要过快，让接收方来得及接收
- 以字节为单位
- 在传输大量数据时，是以 MSS 的大小将数据分割发送。重发时也是以 MSS 为单位
- 没有长度限制，理论上可以无限长，但是为了保证网络的效率，通常TCP数据包的长度不会超过IP数据包的长度，以确保单个TCP数据包不必再分割
  - 能够确保数据不会遗失
  - 缺点过程复杂、实现困难、消耗较多的资源
- 最大消息长度 MSS Maximum Segment Size
  - 建立 TCP 连接的同时，也可以确定发送数据包的单位
  - 最理想情况下，最大消息长度正好是 IP 中不会被分片处理的最大数据长度
  - 以一个段（Segment）为单位，每发送一个段进行一次确认应答的处理，这样的传输方式有一个显著缺点，就是包往返的时间越长通信性能就越低
- 窗口机制
  - 确认应答不再以每个分段，而是以更大单位进行确认，也就是说，发送端主机在发送完一个段之后，不必一直等待确认应答，而是继续发送
  - 窗口大小就是指无需等待确认应答而可以继续发送数据的最大值，这个机制实现了使用大量的缓冲区（临时保存收发数据的场所），通过对多个段同时进行确认应答的功能，而不是每个分段都返回确认应答，从而大幅度缩短发送时间。
  - 在得到确认应答之前，需要在缓冲区保存这部分发送的数据，以便于重发数据
- 在滑动窗口以外的部分包括尚未发送的数据以及已经确认对端已经收到的数据，当数据发出后若如期收到确认应答就不再进行重发，此时数据就会从缓冲区中清除，否则丢失的数据需要进行重发（从缓冲区取）
- 窗口大小
  - TCP 头里有一个字段叫 Advertised window，等于第二部分加上第三部分
  - 接收主机将可以接收缓冲区大小放入字段中通知给发送端。这个字段值越大，说明网络的吞吐量越高
  - 发送端就可以根据这个接收端的处理能力来发送数据，而不会导致接收端处理不过来
  - 实现实际上是操作系统开辟的一个缓存空间，发送方主机在等到确认应答返回之前，必须在缓冲区中保留已发送的数据。如果按期收到确认应答，此时数据就可以从缓存区清除
- 滑动窗口控制
  - 收到确认应答的情况下，将窗口滑动到确认应答中的序列号的位置，这样就可以顺序将多个段同时发送，提高通信性能
  - 应答式交互数据包的往返时间越长，通信的效率就越低。无需等待确认应答，而可以继续发送数据的最大值
  - 通信双方根据接收方的接收情况动态告诉发送端可以发送的数据量，从而实现发送方和接收方的数据收发能力匹配
  - 接收端缓冲区一旦面临数据溢出风险，窗口大小的值也会随之被设置为一个更小的值通知给发送端，从而控制数据发送量。发送端会根据接收端的指示，对发送数据的量进行控制
  - 起到限流作用:当前滑动窗口的大小决定当前 TCP 发送包的速率，而滑动窗口的大小取决于拥塞控制窗口和流量控制窗口的两者间的最小值
  - 接收窗口和发送窗口的大小是相等：并不是完全相等，接收窗口的大小是约等于发送窗口的大小的。滑动窗口并不是一成不变的
  - 发送窗口和接收窗口中所存放的字节数，都是放在操作系统内存缓冲区中的，而操作系统的缓冲区，会被操作系统调整
  - 接收缓存，当数据来到时会先把数据放到缓存中，上层应用等缓存中有数据时就会到缓存中取数据。假如发送方没有限制地不断地向接收方发送数据，接收方的应用程序又没有及时把接收缓存中的数据读走，就会出现缓存溢出，数据丢失的现象，为了解决这个问题，引入流量控制窗口
  - 当接收方比较慢的时候，要防止低能窗口综合征，别空出一个字节来就赶快告诉发送方，然后马上又填满了，可以当窗口太小的时候，不更新窗口，直到达到一定大小，或者缓冲区一半为空，才更新窗口。
- HostB 把当前的**rwnd**值放入报文头部的接收窗口receive window字段中，以此通知HostA自己还有多少可用空间，而HostA则将未确认的数据量控制在rwnd值的范围内，从而避免HostB的接收缓存溢出
- 并不关心链路带宽情况，只关心通信双方的接收发送缓冲区的空间大小，可以说是个速率流量匹配策略
- RcvBuffer是接收区总大小，buffered data是当前已经占用的数据，而free buffer space是当前剩余的空间，rwnd的就是free buffer space区域字节数
- 数据包丢失现象
  - 接收缓存减少，发送方还按照之前商定的窗口大小发送数据，造成发送数据大小超过接收窗口大小，数据包丢失
  - 客户端收到，服务端发送的确认报文和通告窗口报文，尝试减少发送窗口，把窗口的右端向左收缩，此时可用窗口大小就会出现诡异的负值。
  - TCP 规定是不允许同时减少缓存又收缩窗口的，而是采用先收缩窗口，过段时间在减少缓存，这样就可以避免丢包情况
- 窗口关闭潜在危险
  - 当发生窗口关闭时，接收方处理完数据后，会向发送方通告一个窗口非 0 的 ACK 报文，如果这个通告窗口的 ACK 报文在网络中丢失：导致发送方一直等待接收方的非 0 窗口通知，接收方也一直等待发送方的数据，如不不采取措施，这种相互等待的过程，会造成了死锁的现象
  - TCP 为每个连接设有一个持续定时器，只要 TCP 连接一方收到对方的零窗口通知，就启动持续计时器。超时，就会发送窗口探测 ( Window probe ) 报文，而对方在确认这个探测报文时，给出自己现在的接收窗口大小
  - 如果接收窗口仍然为 0，那么收到这个报文的一方就会重新启动持续计时器；
  - 如果接收窗口不是 0，那么死锁的局面就可以被打破了
- 糊涂窗口综合症
  - 如果接收方腾出几个字节并告诉发送方现在有几个字节的窗口，而发送方会义无反顾地发送这几个字节
  - TCP + IP 头有 40 个字节，为传输那几个字节的数据，要达上这么大的开销，这太不经济（超调概念）
  - 解决方案
    - 让接收方不通告小窗口给发送方：当「窗口大小」小于 min (MSS，缓存空间 / 2) ，也就是小于 MSS 与 1/2 缓存大小中的最小值时，就会向发送方通告窗口为 0
    - 让发送方避免发送小数据：使用 Nagle  算法，该算法的思路是延时处理，它满足以下两个条件中的一条才可以发送数据：
      - 要等到窗口大小 >= MSS 或是 数据大小 >= MSS
      - 收到之前发送数据的 ack 回包

###### Nagle 算法

- 用于减少TCP中小包的发送
- 实现
  - 如果应用程序逐个字节的将数据发送到TCP缓存(比如Telnet)，那么TCP就先把第一个字节发出去，把后面到达的自己都缓存起来，当收到第一个字节的确认后，再将缓存中的所有数据组装成一个报文发送出去。减少TCP所用的网络带宽
- 原本为诸如 Telnet 或 rlogin 这样的应用程序而创建的
- 规定 当缓存数据已经到达发送窗口的一半或者报文段的MSS时，则立即发送
- 缺点
  - 默认情况下 Nagle 和延迟 ACK 都是开启的，此时延迟确认和 Nagle 同时使用会大大降低网络性能，因为发送方在等待接收方的ACK，但是接收方却延迟了ACK。因此 Socket 提供提供了TCP_NODELAY选项来禁用Nagle算法

###### 延迟确认

- 通过延迟一定时间(默认40ms)，将多个ACK确认包合并在一起发送，这样减少ACK 确认包在网络中的数量，提高网络性能
- TCP_CORK 禁止发送小包，可以认为是 Nagle 算法的增强，因此TCP_CORK和TCP_NODELAY 恰恰相反
- Socket 设置 TCP_QUICKACK 禁用延迟确认
- TCP_NOPUSH 会设置 CORK算法，表示数据包不会马上传送出去，等到数据包最大时，一次性的传输出去，这样有助于解决网络堵塞
- web 服务器,下载服务器(ftp的发送文件服务器)，需要带宽量比较大的服务器，用TCP_CORK。涉及到交互的服务器，比如ftp的接收命令的服务器，必须使用TCP_NODELAY

##### Congestion Control 拥塞控制

- 避免发送方数据填满整个网络，导致网络拥塞
- 在网络出现拥堵时，如果继续发送大量数据包，可能会导致数据包时延、丢失等，这时 TCP 就会重传数据，但是一重传就会导致网络的负担更重，于是会导致更大的延迟以及更多的丢包，这个情况就会进入恶性循环被不断地放大
- 入选计算机名人堂 Internet Hall of Fame，[Van Jacobson 提出并设计实施了TCP/IP拥塞控制](https://ee.lbl.gov/papers/congavoid.pdf)
- 能最大限度地利用带宽，又不至于让网络环境变得太过拥挤。拥塞影响很大，但是一直低速发包对带宽利用率很低也是很不明智的做法，因此要充分利用带宽就不能过低过高发送数据，而是保持在一个动态稳定的速率来提高带宽利用率
- 避免
  - 包丢失
  - 超时重传
- Congestion Window 拥塞窗口 cwnd
  - LastByteSent - LastByteAcked <= min {cwnd, rwnd} 拥塞窗口和滑动窗口共同控制发送的速度
  - cwnd 和 rwnd 并不冲突，发送方结合rwnd和cwnd来发送数据 swnd = min (cwnd, rwnd)
- 拥塞控制是一个动态过程，既要提高带宽利用率发送尽量多的数据又要避免网络拥堵丢包RTT增大等问题，基于这种高要求并不是单一策略可以搞定的，因此TCP 拥塞控制策略是分阶段分策略综合过程
- 慢启动阀值|门限 slow start threshold ssthresh 65535 个字节
  - 为防止超时重发时，随着包往返导致拥塞窗口快速增长（指数增长），引入的概念
  - cwnd < ssthresh 触发慢启动
    - 一条 TCP 连接开始，cwnd 设置为一个报文段，一次只能发送一个；当收到这一个确认的时候，cwnd 加一，于是一次能够发送两个；当这两个的确认到来的时候，每个确认 cwnd 加一，两个确认 cwnd 加二，是指数性的增长。
  - cwnd >= ssthresh 触发拥塞避免
    - 每收到一个确认后，cwnd 增加 1/cwnd，一次发送八个，当八个确认到来的时候，每个确认增加 1/8，八个确认一共 cwnd 增加 1，于是一次能够发送九个，变成线性增长
- 慢启动 slow start
  - 建立连接后,不要一开始就发送大量数据，先探测一下网络拥塞程度，由小到大逐渐增加拥塞窗口的大小.网络拥堵时，如果通信一开始就发送一个较大量的数据，极有可能导致整个网络的瘫痪
  - 在发送数据包时，将拥塞窗口大小与接收端主机通知的窗口大小做比较,按照它们当中较小的那个值，发送比它还要小的数据量
  - 很快到达一个比较高的发送速率, cwnd 超过 ssthresh，触发拥塞避免
- 拥塞避免 congestion avoidance
  - 将原本慢启动算法指数增长变成线性增长，还是增长阶段，但是增长速度缓慢一些,一个承上启下过程
  - 一直增长着后，网络就会慢慢进入拥塞状况，会出现丢包现象，丢失的数据包会进行超时重传
  - 超时重传
    - RTO(重传超时时间)随着复杂网络环境而动态变化的
    - cwnd 设为 1， ssthresh 设为 cwnd/2，重新开始慢启动，会突然减少数据流的
    - 这种方式太激进了，反应也很强烈，会造成网络卡顿
  - 快速重传 fast retransmit
    - 相比超时重传而言，重发等待时间会降低并且后续尽量避免慢启动，来保证性能损失在最小的程度
    - 当接收端发现丢了一个中间包的时候，发送三次前一个包的 ACK，于是发送端就会快速地重传，不必等待超时再重传。
    - TCP 认为这种情况不严重，因为大部分没丢，只丢了一小部分，cwnd 减半为 cwnd/2，然后 sshthresh = cwnd，当三个包返回的时候，cwnd = sshthresh + 3，还在比较高的值，呈线性增长
    - 更加主动，有利于保证链路的传输性能，但是有研究表明3个ACK的机制同样存在问题
    - 基于对网络状况没有那么糟糕的假设，因此在实际网络确实还算好的时候，快速重传还是很有用的，在很差的网络环境很多算法都很难保证效率的
- 丢包反馈策略问题
  - 丢包即拥塞:现实中网络环境很复杂会存在错误丢包，很多算法无法很好区分拥塞丢包和错误丢包，因此在存在一定错误丢包的前提下在某些网络场景中并不能充分利用带宽比如：
    - 全球最牛的防火墙 GWF 的随机丢包策略
    - 网路中由于多路径衰落（multi-path fading）所造成的信号衰减（signal degradation）
    - 通道阻塞造成的丢包（packet drop），再者损坏的封包（corrupted packets）被拒绝通过
    - 有缺陷的网路硬件、网路驱动软件发生故障
    - 信号的信噪比（SNR）的影响
  - 缓冲区膨胀问题 BufferBloat  经济中的加息
    - 网络连接中路由器、交换机、核心网设备等等为了平滑网络波动而存在缓冲区，这些缓存区就像输液管的膨胀部分让数据更加平稳，但是Loss-Based策略在最初就像网络中发生数据类似于灌水，此时是将Buffer全部算在内的，一旦buffer满了，就可能出现RTT增加丢包等问题，就相当于有的容量本不该算在其中，但是策略是基于包含Buffer进行预测的，特别地在深缓冲区网络就会出现一些问题。
    - 网络负载高无丢包：假设网络中负载已经很高了，只要没有丢包事件出现，算法就不会主动减窗降低发送速率，这种情况下虽然充分利用了网络带宽，同时由于一直没有丢包事件出现发送方仍然在加窗，表现出较强的网络带宽侵略性，加重了网络负载压力
    - 高负载丢包： 高负载无丢包情况下算法一直加窗，这样可以预测丢包事件可能很快就出现了，一旦丢包出现窗口将呈现乘性减少，由高位发送速率迅速降低会造成整个网络的瞬时抖动性，总体呈现较大的锯齿状波动。
    - 低负载高延时丢包：在某些弱网环境下RTT会增加甚至出现非拥塞引起丢包，此时基于丢包反馈的拥塞算法的窗口会比较小，对带宽的利用率很低，吞吐量下降很明显，但是实际上网络负载并不高，所以在弱网环境下效果并不是非常理想
    - 只要填满管道就可以了，不应该接着填直到连缓存也填满。
    - RTT 增大影响了比如CUBIC这类拥塞控制算法的慢启动等阶段，慢启动阶段每经过1个RTT周期拥塞窗口cwnd将加倍，但是更大的RTT就意味着发送方以很低的速率发送数据，更多的时间是空闲的，发包的加速度极大将低了，所以整个吞吐量就下降很明显
- 优化
  - Sysctl variable tcp_max_syn_backlog and socket variable somax_conn determines how many connections for which the kernel can complete 3 way handshake before app calling accept syscall.Once the backlog is full, new connections stay in SYN_RCVD state (when you run netstat) till the application calls accept syscall
  - Apps can run out of file descriptors if there are too many short lived connections. Digging through tcp_reuse and tcp_recycle can help reduce time spent in the time wait state(it has its own risk). Making apps reuse a pool of connections instead of creating ad hoc connection can also help
  - too many sockets in Close_wait state is a problem on application
  - retransmissions can be a problem more on network or on OS stack than the application itself
- AIMD 线性增加乘性减少算法
  - 一个反馈控制算法，因其在TCP拥塞控制中的使用而广为人知，将线性增加拥塞窗口和拥塞时乘性减少窗口相结合，基于AIMD的多个连接理想状态下会达到最终收敛，共享相同数量的网络带宽，与其相关的乘性增乘性减MIMD策略和增性加增性减少AIAD都无法保证稳定性
  - 弱网环境下，尤其是移动互联网中之前的基于AIMD的拥塞控制策略可能会由于丢包的出现而大幅降低网络吞吐量，从而对网络带宽的利用率也大大下降，这时采用更加激进的控制策略，或许可以获得更好的效果和用户体验
- 深度包检测 DPI  Deep Packet Inspection
  - 识别TCP/IP网络协议中各种各样的报文，来进行流量管控和分析，在网络安全领域应用很多，属于通信&互联网领域的交叉业务
- 一个TCP会话使用的拥塞控制算法只与局部有关。所以，两个TCP系统可以在TCP会话的两边使用不同的拥塞控制算法。换句话说：服务器(发送方)，可以在本地启用BBR，而客户端不需要知道BBR，也不需要启用BBR
- 在没有丢包的情况下，Cubic和BBR对于这些较长时延的链路都有很好的表现。而在中度丢包的情况下，BBR的表现就非常突出了
	- 出现丢包的情况下，BBR将会大放异彩，帮助维护更好的网络数据传输

![Alt text](../_static/tcp_block_control.png "Optional title")

```sh
# 客户端和服务端都是 CentOs 6.5 ，Linux 内核版本 2.6.32
# 服务端 Nginx 服务 IP 192.168.3.200，端口为 8088
# 客户端 IP 192.168.3.100

wrk -t 6 -c 30000 -d 20s http://192.168.33.10
date;netstat -s | grep overflowed # 查看全连接队列溢出的次数，注意这个是累计值。可以隔几秒钟执行下，如果这个数字一直在增加的话肯定全连接队列偶尔满了

sudo apt install hping3
hping3 -S -p 80 --flood 192.168.33.10

netstat -s | grep "SYNs to LISTEN" # 查看累计
```

```sh
# 查看可用拥塞算法
sysctl net.ipv4.tcp_available_congestion_control

# 查看使用哪一种
sysctl net.ipv4.tcp_congestion_control

# 修改
sudo sysctl -w net.ipv4.tcp_congestion_control=cubic
```

###### [TCP BBR Bottleneck Bandwidth and Round-trip propagation time](https://github.com/google/bbr)

- [论文](https://queue.acm.org/detail.cfm?id=3022184)
- 目的是要尽量跑满带宽，并且尽量不要有排队的情况，效果并不比速锐差。旨在恢复期间提高发送数据的准确性，该算法确保恢复后的拥塞窗口大小尽可能接近慢启动阈值。
- Linux kernel 4.9+ 已支持 tcp_bbr,安装 Hardware Enablement Stack (HWE)，自动更新内核
- 使用BBR，可以获得显著的网络吞吐量的提升和延迟的降低。
	- 吞吐量的改善在远距离路径上尤为明显，比如跨太平洋的文件或者大数据的传输，尤其是在有轻微丢包的网络条件下。
	- 延迟的改善主要体现在最后一公里的路径上，而这一路径经常受到缓冲膨胀（Bufferbloat）的影响。
	- 所谓“缓冲膨胀”指的网络设备或者系统不必要地设计了过大的缓冲区。当网络链路拥塞时，就会发生缓冲膨胀，从而导致数据包在这些超大缓冲区中长时间排队。
    - 在先进先出队列系统中，过大的缓冲区会导致更长的队列和更高的延迟，并且不会提高网络吞吐量。由于BBR并不会试图填满缓冲区，所以在避免缓冲区膨胀方面往往会有更好的表现。
	- 在Google进行的测试中，能将平均延迟降低3~10%恢复超时减少5%
	- Google在YouTube上应用该算法，将全球平均的YouTube网络吞吐量提高了4%，之后移植入Linux内核4.9版本,对QUIC可用
	- 长肥网络|长肥管道 把具有长RTT往返时间和高带宽的网络成，带宽延时积BDP很大，这种网络理论上吞吐量很大也是研究的重点
	- BBR对所谓的“长肥网络”（带宽延迟积大、丢包率高的网络）非常有效，在CDN和视频应用等场景下也被证明有很好的表现
- 由Google设计于2016年发布的拥塞算法，以往大部分拥塞算法是基于丢包来作为降低传输速率的信号，该算法认为随着网络接口控制器逐渐进入千兆速度时，分组丢失不应该被认为是识别拥塞的主要决定因素,基于模型的拥塞控制算法能有更高的吞吐量和更低的延迟，可以用BBR来替代其他流行的拥塞算法
  - 基于丢包反馈的协议是一种被动式的拥塞控制机制，其依据网络中的丢包事件来做网络拥塞判断。即便网络中的负载很高时，只要没有产生拥塞丢包，协议就不会主动降低自己的发送速度。
- BBR 基于模型主动探测
  - 不再基于丢包判断也不再使用AIMD线性增乘性减策略来维护拥塞窗口，而是分别采样估计极大带宽和极小延时，并用二者乘积作为发送窗口
  - 引入 Pacing Rate 限制数据发送速率，配合 cwnd 使用来降低冲击,有更高的吞吐量和更低的延迟
    - TCP Pacing机制 将拥塞控制中数据包的做平滑发送处理，避免数据的突发降低网络抖动
  - 使用网络最近出站数据分组当时的最大带宽和往返时间来创建网络的显式模型,数据包传输的每个累积或选择性确认用于生成记录在数据包传输过程和确认返回期间的时间内所传送数据量的采样率
  - 这种协议可以最大程度的利用网络剩余带宽，提高吞吐量。然而，由于基于丢包反馈协议在网络近饱和状态下所表现出来的侵略性，一方面大大提高了网络的带宽利用率；但另一方面，对于基于丢包反馈的拥塞控制协议来说，大大提高网络利用率同时意味着下一次拥塞丢包事件为期不远了，所以这些协议在提高网络带宽利用率的同时也间接加大了网络的丢包率，造成整个网络的抖动性加剧
- BDP 带宽延时积 Bandwidth-Delay Product
  - 带宽单位是bps(bit per second)，延时的单位是s，BDP 量纲单位就是bit，衡量一段时间内链路的数据量的指标。
  - 可以形象理解为水管灌水问题，带宽就是水管的水流速度立方米/s，延时就是灌水时间单位s，二者乘积可以知道当前水管内存储的水量了，
  - BBR 算法的一个关键指标
- TCP 带宽和延时的测量
  - 采用交替采样测量带宽和延时乘积指标，取一段时间内的带宽极大值和延时极小值作为估计值
- 主动的闭环反馈系统
  - 根据带宽和RTT延时来不断动态探索寻找合适的发送速率和发送量
  - 通过不断地加快发送速度，将管道填满，但是不要填满中间设备的缓存，因为这样时延会增加，在这个平衡点可以很好的达到高带宽和低时延的平衡。
    - app limit 应用限制阶段：应用程序开始发送数据，目前网络通畅RTT基本保持固定且很小，发送速率与RTT成反比，因此发送速率也是线性增加的，可以简单认为这个阶段有效带宽并没有达到上限，RTT是几乎固定的没有明显增长。
    - band limit 带宽限制阶段： 随着发送速率提高，网络中的数据包越来越多开始占用链路Buffer，此时RTT开始增加发送速率不再上升，有效带宽开始出现瓶颈，但是此时链路中的缓存区并没有占满，因此数据还在增加，RTT也开始增加。
    - buffer limit 缓冲区限制阶段：随着链路中 Buffer 被占满，开始出现丢包，这也是探测到的最大带宽，这个节点BDP+BufferSize也是基于丢包的控制策略的作用点。
- 过程
  - StartUp 慢启动阶段
    - 类似于 CUBIC 慢启动，同样是进行探测式加速.
    - 区别在于BBR慢启动使用2ln2的增益加速，过程中即使发生丢包也不会引起速率的降低，而是依据返回的确认数据包来判断带宽增长，直到带宽不再增长时就停止慢启动而进入下一个阶段，
    - 需要注意的是在寻找最大带宽的过程中产生了多余的2BDP的数据量，英文原文解释： To handle Internet link bandwidths spanning 12 orders of magnitude, Startup implements a binary search for BtlBw by using a gain of 2/ln2 to double the sending rate while delivery rate is increasing. This discovers BtlBw in log2BDP RTTs but creates up to 2BDP excess queue in the process.
    - Drain 排空阶段
      - 为把慢启动结束时多余的2BDP的数据量清空，此阶段发送速率开始下降，也就是单位时间发送的数据包数量在下降，直到未确认的数据包数量<BDP时认为已经排空，也可以认为是RTT不再下降为止，排空阶段结束。
    - ProbeBW 带宽探测阶段
      - 经过慢启动和排空之后，目前发送方进入稳定状态进行数据的发送，由于网络带宽的变化要比RTT更为频繁，
      - 因此ProbeBW阶段也是BBR的主要阶段，在探测期中增加发包速率如果数据包ACK并没有受影响那么就继续增加，探测到带宽降低时也进行发包速率下降。
    - ProbeRTT 延时探测阶段
      - 前面三个过程在运行时都可能进入ProbeRTT阶段，当某个设定时间内都没有更新最小延时状态下开始降低数据包发送量，试图探测到更小的MinRTT，探测完成之后再根据最新数据来确定进入慢启动还是ProbeBW阶段
- 测试
  - 在一个高延迟的路径上，仅仅是少量的数据包丢失（1.5%）就会产生了巨大的影响。
  - 只有BBR在任何超过1.5%的丢包损失时都能保持一个不错的吞吐量数字。
- 缺点
	- 倾向于抢占Cubic算法的带宽，在网络公平性上明显存在不足
	- BBR的机制会导致高重传率
	- 在Wi-Fi环境下用户的网速明显变慢
- BBRv2
	- 改进包括了还使用聚合/运行中的参数增强了网络建模，并增加了对ECN(显式拥塞通知)的支持等

```sh
uname -r # 看看是不是内核 >= 4.9
lsmod | grep bbr # 查看
sudo modprobe tcp_bbr
echo "tcp_bbr" | sudo tee --append /etc/modules-load.d/modules.conf

echo "net.core.default_qdisc=fq" | sudo tee --append /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee --append /etc/sysctl.conf

sudo sysctl -p # 配置生效

sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
lsmod | grep bbr

apt install --install-recommends linux-generic-hwe-16.04
sudo apt autoremove

sudo sysctl -w net.ipv4.tcp_congestion_control=bbr2

## 模拟丢包与延迟
# 增加 50ms 延迟
sudo tc qdisc replace dev eth0 root netem latency 50ms
# 取消上述的设置可以使用这个命令 
sudo tc qdisc del dev eth0 root

# 模拟丢包
sudo tc qdisc replace dev eth0 root netem loss 1.5% latency 50ms
```

#### [TCP KeepAlive 长连接](http://www.tldp.org/HOWTO/html_single/TCP-Keepalive-HOWTO/)

- 短连接
  - 通信双方有数据交互时，就建立一个TCP连接，数据发送完成后，则断开此TCP连接。每次都经历建立连接需要三次握手、断开连接需要四次挥手。
  - 每一次链接建立需要这种经常性的开销，而其并不带有实际有用的数据，只是保证链接的可靠性，因此 HTTP/1.1 提出可持续链接的实现方法
- 长连接
  - HTTP/1.1 只建立一次 TCP 链接而重复地使用传输一系列的请求/响应消息，减少链接建立的次数和经常性的链接开销
  - 如果连接双方如果没有一方主动断开都不会断开TCP连接，减少每次建立HTTP连接时进行TCP连接的消耗
  - 存活检测
    - 隔一段时间给连接对端发送一个探测包，如果收到对方回应 ACK，则认为连接还是存活的
    - 在超过一定重试次数之后还是没有收到对方的回应，则丢弃该 TCP 连接
- 半开连接
  - 在长时间无数据交互时间段内，交互双方都有可能出现掉电、死机、异常重启等各种意外
  - 当这些意外发生之后，这些 TCP 连接并未来得及正常释放，
  - 在软件层面上，连接的另一方并不知道对端的情况，会一直维护这个连接，长时间的积累会导致非常多的半打开连接，造成端系统资源的消耗和浪费
  - linux 默认配置2小时，可以配置修改
  - 长连接中间件，需要处理这个细节
- 关闭连接:最好由客户端主动发起，TIME_WAIT这个状态最好不要在服务器端，减少占用资源
- 建议：
  - 在客户端数量少场景一般使用长连接。后端中间件、微服务之间通信最好使用长连接。如：数据库连接，duboo默认协议等
  - 大型web、app应用，使用http短连接（http1.1的keep alive变相的支持长连接，但还是串行请求/响应交互）。http2.0支持真正的长连接
  - 长连接会对服务端耗费更多的资源，上百万用户，每个用户独占一个连接，对服务端压力多大，成本多高。IM、push应用会使用长连接，但是会做很多优化工作
  - 由于 https 需要加解密运算等，最好使用http2.0（强制ssl），传输性能很好。但是服务端需要维持更多的连接
- 局限
  - TCP KeepAlive 监测方式是发送一个 probe 包，会给网络带来额外流量
  - TCP KeepAlive  只能在内核层级监测连接的存活与否，而连接的存活不一定代表服务的可用。例如当一个服务器 CPU 进程服务器占用达到 100%，已经卡死不能响应请求了，此时 TCP KeepAlive 依然会认为连接是存活的。
  - 因此 TCP KeepAlive 对于应用层程序的价值是相对较小的。需要做连接保活的应用层程序，例如 QQ，往往会在应用层实现自己的心跳功能。

#### TIME_WAIT

- `TIME_WAIT` 状态
  - TCP 连接中，主动关闭连接的一方出现的状态（收到 FIN 命令，进入 TIME_WAIT 状态，并返回 ACK 命令）
  - 保持 2 个 MSL 时间，即，4 分钟；（MSL 为 2 分钟）
  - 默认会持续 2 MSL（报文的最大生存时间），一般是 2x2 mins
  - TCP 连接占用的端口，无法被再次使用,TCP 端口数量，上限是 6.5w（65535，16 bit）
  - 大量 time_wait 状态存在，会导致新建 TCP 连接会出错，address already in use : connect 异常
- TIME_WAIT 状态存在必要性：
  - 可靠实现 TCP 全双工连接终止：最后 ACK 是由「主动关闭连接」的一端发出的，如果这个 ACK 丢失，则对方会重发 FIN 请求，因此，在主动关闭连接的一段，需要维护一个 time_wait 状态，处理对方重发 FIN 请求
  - 处理延迟到达报文：由于路由器可能抖动，TCP 报文会延迟到达，为了避免「延迟到达的 TCP 报文」被误认为是「新 TCP 连接」的数据，需要在允许新创建 TCP 连接之前，保持一个不可用的状态，等待所有延迟报文的消失，一般设置为 2 倍的 MSL（报文的最大生存时间），解决「延迟达到的 TCP 报文」问题
- 现实场景
  - 服务器端，一般设置：不允许「主动关闭连接」
  - 但 HTTP 请求中，http 头部 connection 参数，可能设置为 close，则服务端处理完请求会主动关闭 TCP 连接
  - 现在浏览器中， HTTP 请求 connection 参数，一般都设置为 keep-alive
  - Nginx 反向代理场景中，可能出现大量短链接，服务器端，可能存在
- 高并发场景，会出现批量 TIME_WAIT 的 TCP 连接
  - 每一个 time_wait 状态，都会占用一个「本地端口」，上限为 65535(16 bit，2 Byte)
  - 当大量连接处于 time_wait 时，新建立 TCP 连接会出错，address already in use : connect 异常
- 原因
  - 大量的短连接存在
  - 特别是 HTTP 请求中，如果 connection 头部取值被设置为 close 时，基本都由「服务端」发起主动关闭连接
  - TCP 四次挥手关闭连接机制中，为了保证 ACK 重发和丢弃延迟数据，设置 time_wait 为 2 倍的 MSL（报文最大存活时间）
- 解决
  - 客户端，HTTP 请求的头部，connection 设置为 keep-alive，保持存活一段时间
  - 服务器端允许 time_wait 状态的 socket 被重用 `net.ipv4.tcp_timestamps=1 net.ipv4.tcp_tw_reuse = 1`
  - 缩减 time_wait 时间，设置为 1 MSL（即，2 mins）

```sh
netstat -nat | grep TIME_WAIT
netstat -nat | grep -E "TIME_WAIT|Local Address"

# 统计各种连接数量
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
```

#### SYN 攻击 SYN Flood

- 一种典型的 DoS/DDoS 攻击
  - 在三次握手过程中，服务器发送 SYN-ACK 之后，收到客户端 ACK 之前 TCP 连接称为半连接(half-open connect)。服务器处于 SYN_RCVD 状态.服务端需要 63s 内保持这个资源
  - 攻击客户端在短时间内伪造大量不存在的IP地址，向服务器不断地发送SYN包，服务器回复确认包，并等待客户的确认。
  - 由于源地址是不存在的，服务器需要不断的重发直至超时，伪造SYN包将长时间占用未连接队列，正常SYN请求被丢弃，导致目标系统运行缓慢，严重者会引起网络堵塞甚至系统瘫痪。
- 检测 SYN 攻击
  - 在服务器上看到大量半连接状态时，特别是源IP地址是随机的，基本上可以断定这是一次SYN攻击
  - 在 Linux/Unix 上可以使用系统自带的 netstats 命令来检测 SYN 攻击
- 防御：不能完全被阻止，除非将TCP协议重新设计。所做的是尽可能减轻危害
  - 开启 tcp_syncookies 功能
  - 缩短超时（SYN Timeout）时间
  - 过滤网关防护
  - 增大半连接队列连接数
    - 增大 `echo 1024 > /proc/sys/net/ipv4/tcp_max_syn_backlog`
    - `echo 1024 > /proc/sys/net/core/somaxconn`
    - nginx 中 blacklog
  - 减少 SYN+ACK 重传次数

#### 粘包，封包与拆包

- 封包
  - 给一段数据加上包头，数据包分为包头和包体两部分内容了（过滤非法包时封包会加入"包尾"内容）
  - 包头其实上是个大小固定的结构体，其中有个结构体成员变量表示包体的长度，这是个很重要的变量。其他的结构体成员可根据需要自己定义。根据包头长度固定以及包头中含有包体长度的变量就能正确的拆分出一个完整的数据包。
- 分包
  - 指的是在发生一个消息(message)或一帧(frame)数据时，通过一定的处理，让接收方能从字节流中识别并截取(还原)出一个个消息
  - 在 TCP 上做应用层分包是网络编程的基本需求
  - TCP 发送机制
    - TCP 维持一个变量，等于最大报文段长度 MSS。只要缓存中存放的数据达到 MSS 字节时，就组装成一个 TCP 报文段发送出去
    - 由发送方的应用进程指明要求发送报文段，即 TCP 支持的推送(push)操作
    - 发送方的一个计时器期限到了，把当前已有的缓存数据装入报文段(但长度不能超过 MSS)发送出去
  - 短连接分包: 对于短连接的 TCP 服务，分包不是一个问题，只要发送方主动关闭连接，就表示一个消息发送完毕，接收方 read() 返回0，从而知道消息的结尾
  - 长连接分包
    - 使用特殊字符或字符串作为消息边界，例如 HTTP 协议的 headers 以 `\r\n` 为字段的分隔符
    - 最常见做法 在每条消息的头部加一个长度字段，这恐怕是
    - 利用消息本身的格式来分包，例如 XML 格式的消息中`  <root>...</root> ` 的配对，或者 JSON 格式中的 `{ ... }` 配对。解析这种消息格式通常会用到状态机(state machine)
  - 复杂分包
    - 假如消息格式非常简单，“消息”本身是一个字符串，每条消息有一个4字节的头部，以网络序存放字符串的长度。消息直接没有间隙，字符串也不要求以 '`\0`' 结尾
- "粘包"可发生在发送端也可发生在接收端：
  - 由Nagle算法造成发送端粘包：Nagle算法是一种改善网络传输效率的算法。简单的说,，当提交一段数据给TCP发送时，TCP并不立刻发送此段数据，而是等待一小段时间,看看在等待期间是否还有要发送的数据，若有则会一次把这两段数据发送出去。
  - 接收端接收不及时造成的接收端粘包：TCP会把接收到的数据存在自己的缓冲区中，然后通知应用层取数据。当应用层由于某些原因不能及时的把TCP的数据取出来，就会造成TCP缓冲区中存放了多段数据。

#### 缺点

- 延迟大，传输效率比 UDP 低
  - 流量控制和拥塞控制确保措施会导致延迟
  - 应答机制中一旦发生丢包，TCP 会将后续包缓存起来，等前面的包重传并接收到后再继续发送，延迟会越来越大

### UDP User Data Protocol 用户数据报协议

- 为应用进程提供端到端的通信服务
- UDP 不提供复杂的控制机制，利用 IP 提供面向无连接的简单消息传输
  - 无连接的。数据报（类似于数据包）只在数据报级别有保证。数据报可能会无序的到达目的地，也有可能会遗失。UDP 不支持拥塞控制。虽然不如 TCP 那样有保证，但 UDP 通常效率更高。
  - 可以通过广播将数据报发送至子网内的所有设备。这对 DHCP 很有用，因为子网内的设备还没有分配 IP 地址，而 IP 对于 TCP 是必须的。
  - 可靠性更低但适合用在网络电话、视频聊天，流媒体和实时多人游戏上。
  - 以下情况使用 UDP 代替 TCP：
    - 需要低延迟
    - 相对于数据丢失更糟的是数据延迟
    - 想实现自己的错误校正方法
  - 协议
    - DNS
    - TFTP
    - SNMP
    - NFS
- 连接:用于保证可靠性和流量控制维护的某些状态信息，这些信息的组合，包括Socket、序列号和窗口大小
  - Socket：由 IP 地址和端口号组成
  - 序列号：用来解决乱序问题等
  - 窗口大小：用来做流量控制
- 提供面向无连接的非可靠性传输
- 不能保证消息一定会按顺序到达，传输途中如果出现丢包，UDP 不负责进行重发，包的到达顺序错乱时，UDP 也没有纠正功能
- 特性
  - UDP 缺乏可靠性。本身不提供确认，序列号，超时重传等机制。UDP 数据报可能在网络中被复制，被重新排序。即 UDP 不保证数据报会到达其最终目的地，也不保证各个数据报的先后顺序，也不保证每个数据报只到达一次
  - UDP 数据报是有长度的。每个 UDP 数据报都有长度，如果一个数据报正确地到达目的地，那么该数据报的长度将随数据一起传递给接收方。而 TCP 是一个字节流协议，没有任何（协议上的）记录边界。是面向报文的，发送方的 UDP 对应用程序交下来的报文，在添加首部后就向下交付 IP 层。UDP 对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界
  - UDP 是无连接的。UDP 客户和服务器之前不必存在长期的关系。UDP 发送数据报之前也不需要经过握手创建连接的过程。
  - UDP 支持多播和广播。
  - 面向非连接 不可靠的传输层协议
  - 提供有限的差错检验功能
  - 目的是希望以最小的开销来达到网络环境中的进程通信目的
  - 能够支持容忍数据包丢失的带宽密集型应用程序
  - 具有低延迟特点
  - 能够发送大量数据包
  - 适用于一次只传送少量数据、对可靠性要求不高的应用环境
  - 网络数据大多为短消息
  - 拥有大量Client
  - 对数据安全性无特殊要求
  - 网络负担非常重，但对响应速度要求高
- 面向报文：应用层交给UDP多长的报文，UDP就照样发送，即一次发送一个报文。因此，应用程序必须选择合适大小的报文。若报文太长，则IP层需要分片，降低效率。若太短，会是IP太小
- 不为IP提供可靠性、流控或差错恢复功能,让广播和细节控制交给应用的通信传输
- 首部开销小，只有8个字节:因为UDP不需要应答，所以来源端口是可选的，如果来源端口不用，那么置为零
- 支持应用层协议
  - NFS（网络文件系统）
  - SNMP（简单网络管理协议）
  - DNS（主域名称系统）
  - TFTP（通用文件传输协议）
  - 动态主机配置协议（DHCP）
  - 路由信息协议（RIP）
  - 自举协议（BOOTP）
  - 实时游戏（自定义重传策略，能够把丢包产生的延迟降到最低，尽量减少网络问题对游戏性造成的影响）

#### 编程步骤

- 服务器端
  - socket() 创建socket
  - setsockopt() 设置socket属性，可选
  - bind() 绑定IP地址、端口等信息到socket上
  - recvfrom() 循环接收数据,传入 IP 地址和端口
  - 关闭网络连接
- 客户端
  - socket() 创建socket
  - setsockopt() 设置socket属性，可选
  - bind() 绑定IP地址、端口等信息到socket上
  - sendto()发送数据，传入 IP 地址和端口
  - 关闭网络连接

#### 特点

- 沟通简单 没有复杂数据结构，相信网络通路默认就是很容易送达的，不容易被丢弃的。

- 轻信他人 谁都可以传给他数据，他也可以传给任何人数据，甚至可以同时传给多个人数据

- 不会根据网络的情况进行发包的拥塞控制，无论网络丢包丢成啥样了，它该怎么发还怎么发

- 优势:简单，容易实现
  - 对握手过程进行精简，减少网络通信往返次数
  - 能够对TLS加解密过程进行优化

- 缺点是可靠性较差，一旦数据包发出，无法知道对方是否收到。
  - Tweaking sysctl variables for rmem and wmem like we did for UDP can improve throughput of sender and receiver.
  - 没有拥塞控制： 出现网络拥堵，无法进行流量控制等避免避免网络拥塞的行为

#### 场景

- 需要资源少，在网络情况比较好的内网，或者对于丢包不敏感的应用
  - DHCP 一般的获取 IP 地址都是内网请求，而且一次获取不到 IP 又没事，过一会儿还有机会
  - TFTP
- 不需要一对一沟通，建立连接，而是可以广播多播应用
- 需要处理速度快，时延低，可以容忍少数丢包，但是要求即便网络拥塞，也毫不退缩，一往无前的时候
  - 视频、音频等多媒体即时通信（少量的丢包不影响通信质量）
- 实例
  - QUIC
  - 流媒体直播协议 RTMP
    - 在网络不好的情况下，应用希望选择性的丢帧。
  - 实时游戏
  - 物联网
  - 移动通信领域

#### UDP 包头

- 16 bit 源端口号
- 16 bit 目的端口号
- 16 bit UDP 长度
- 16 bit UDP 校验和

### TCP vs UDP

- TCP 面向连接(Connection oriented)，UDP无连接(Connection less)协议
  - TCP  传输数据前先要建立连接。在客户端和服务端维护连接，而建立一定的数据结构来维护双方交互的状态，用这样的数据结构来保证所谓的面向连接的特性。
  - UDP 不需要连接，即刻传输数据。
- 首部开销
  - TCP 首部长度较长，会有一定的开销，首部在没有使用「选项」字段时是 20 个字节，如果使用了「选项」字段则会变长的
  - UDP 首部只有 8 个字节，并且是固定不变的，开销较小
- TCP 重量级的，UDP轻量级的
  - TCP要建立连接、保证可靠性和有序性，就会传输更多的信息，如TCP头部需要20字节
  - UDP头部只要8个字节
- TCP 面向字节流，UDP 基于数据报
  - TCP 通过字节流传输，没头没尾
  - UDP 中每一个包都是单独的，数据报模式
- 可靠性
  - TCP 可靠交付数据的，数据可以无差错、不丢失、不重复、按序到达
  - UDP 尽最大努力交付，不保证可靠交付数据
- TCP 有状态服务，UDP 无状态服务
- TCP 有序，UDP 无序 消息在传输过程中可能会乱序，后发送的消息可能会先到达，TCP会对其进行重排序，UDP不会。
- 服务对象
  - TCP  一对一的两点服务，即一条连接只有两个端点
  - UDP 支持一对一、一对多、多对多的交互通信
- 拥塞控制、流量控制
  - TCP 有拥塞控制和流量控制机制，保证数据传输的安全性。
  - UDP 则没有，即使网络非常拥堵了，也不会影响 UDP 的发送速率,网络出现拥塞不会使源主机的发送速率降低
- TCP 逻辑通信信道是全双工可靠信道，UDP则是不可靠信道
- 场景
  - FTP HTTP / HTTPS
  - 包总量较少的通信，如 DNS 、SNMP 等 视频、音频等多媒体通信 广播通信
- 编程区别
  - socket()参数不同
  - UDP Server 不需要调用listen和accept
  - UDP 收发数据用sendto/recvfrom函数
  - UDP：在sendto/recvfrom函数中每次均需指定地址信息
  - UDP：shutdown函数无效
  - TCP：地址信息在connect/accept时确定

![TCP与UDP对比](../_static/TCPvsUDP.png)

### 4层交换机 Layer 4 switching

### 状态防火墙 stateful firewall

### route

```sh
# 查看路由表
route

# 添加一条路由信息
# 为 `eth0` 接口添加一个地址范围（从 `169.254.0.0` 开始到 `169.254.0.255` 结束）的路由。路由协议设置为“静态”，表示作为管理员创建了这个路由，作为对该范围内的任何动态路由进行覆盖。
sudo ip route \
	add 169.254.0.0/24 \
	dev eth0 \
	proto static
```

### [iperf](https://github.com/esnet/iperf)

- iperf3: A TCP, UDP, and SCTP network bandwidth measurement tool <https://iperf.fr/>
- 测试最大 TCP 和 UDP 带宽性能，具有多种参数和 UDP 特性，可以根据需要调整，可以报告带宽、延迟抖动和数据包丢失。
- 共用选项
  - -u  –udp：使用 UDP 方式而不是 TCP 方式。需要客户端与服务器端同时使用此参数。
  - -p  –port : 设置端口，与服务器端的监听端口一致。默认是 5001 端口。
  - -l  –len : 设置读写缓冲区的长度。TCP 方式默认为 8KB，UDP 方式默认为 1470 字节。
  - -w  –window : 设置套接字缓冲区为指定大小。对于 TCP 方式，此设置为 TCP 窗口大小。对于 UDP 方式，此设置为接受 UDP 数据包的缓冲区大小，限制可以接受数据包的最大值。
  - -m  –print_mss : 输出 TCP MSS 值（通过 TCP_MAXSEG 支持）。MSS 值一般比 MTU 值小 40 字节。通常情况
- 服务器端专用选项
  - -s  –server : iperf 服务器模式
  - -c  –client host : 如果 iperf 运行在服务器模式，并且用 - c 参数指定一个主机，那么 iperf 将只接受指定主机的连接。此参数不能工作于 UDP 模式。
  - -P  –parallel： 服务器关闭之前保持的连接数。默认是 0，这意味着永远接受连接。
- 客户端端专用选项
  - -c  –client host ： 运行 iperf 的客户端模式，连接到指定的 iperf 服务器端。
  - -b  –bandwidth ：UDP 模式使用的带宽，必须配合 - u 参数，默认值是 1 Mbit/sec。
  - -d  –dualtest ： 运行双测试模式。这将使服务器端反向连接到客户端，使用 - L 参数中指定的端口（或默认使用客户端连接到服务器端的端口）。这些在操作的同时就立即完成了。如果你想要一个交互的测试，请尝试 - r 参数。
  - -r  –tradeoff ： 往复测试模式。当客户端到服务器端的测试结束时，服务器端通过 - l 选项指定的端口（或默认为客户端连接到服务器端的端口），反向连接至客户端。当客户端连接终止时，反向连接随即开始。如果需要同时进行双向测试，请尝试 - d 参数。
  - -L  –listenport ： 指指定服务端反向连接到客户端时使用的端口。默认使用客户端连接至服务端的端口。
  - -t  –time ： 设置传输的总时间。iperf 在指定的时间内，重复的发送指定长度的数据包。默认是 10 秒钟。
  - -P  –parallel： 线程数。指定客户端与服务端之间使用的线程数。默认是 1 线程。需要客户端与服务器端同时使用此参数。
  - -p：后接服务端监听的端口
  - -i：设置带宽报告的时间间隔，单位为秒
  - -w：设置 tcp 窗口大小，一般可以不用设置，默认即可

```sh
# 服务器端
iperf -u -s

# 客户端：
# /* 在 udp 模式下，以 100Mbps 为数据发送速率，客户端到服务器 192.168.1.1 上传带宽测试，测试时间为 60 秒 */
iperf -u -c 192.168.1.1 -b 100M -t 60

# /* 客户端以 5Mbps 为数据发送速率, 同时向服务器端发起 30 个连接线程 */
iperf -u -c 192.168.1.1 -b 5M -P 30 -t 60

# /* 以 100M 为数据发送速率，进行上下行带宽测试,-L 参数指定本端双测试监听的端口 */
iperf -u -c 192.168.1.1 -b 100M -d -t 60 -L 30000

# TCP 模式
# 服务器端：
iperf -s

# 客户端：
# /* 在 tcp 模式下，客户端到服务器 192.168.1.1 上传带宽测试，测试时间为 60 秒 */
iperf -c 192.168.1.1 -t 60

# /* 进行上下行带宽测试 */
iperf -c 192.168.1.1 -d -t 60

# /* 测试单线程 TCP*/
iperf –c 192.168.1.1 –p 12345 –i 1 –t 10 –w 20K

 # 对应服务器端：
iperf –s –p 12345 –i 1 –t 10 –m -y

/* 测试多线程 TCP: 客户端同时向服务器端发起 30 个连接线程 */
iperf -c 192.168.1.1 -P 30 -t 60
```

## Network layer 网络层

- IP 负责将包发送至接受者
- 路由机制（routing）:每个网卡都有自己固定的 MAC 地址，当这个网卡接入到不同的网络，每次都可以再分配不同的“网络地址”。通过“网络地址”可以看出这个网卡属于哪个网络
  - A 主机的协议栈先判断“A B 两个地址”是否在同一个子网（“子网掩码”就是用来干这事儿滴）
    - 如果是同一个子网，直接发给对方；如果不是同一个子网，发给本子网的【默认网关】。（此处所说的“网关”指“3层网关/网络层网关”）
  - 对于“默认网关”，有可能自己就是路由器；也可能自己不是路由器，但与其它路由器相连。也就是说，“默认网关”要么自己对数据包进行路由，要么丢给能进行路由的另一台设备。（万一找不到能路由的设备，这个数据就被丢弃，于是网络通讯出错）
  - 当数据到达某个路由器之后，有如下几种可能
    - 该路由器正好是 B 所在子网的网关（与 B 直连），那就把数据包丢给 B，路由过程就结束
    - 亦或者，路由器会把数据包丢给另一个路由器（另一个路由器再丢给另一个路由器） ...... 如此循环往复，最终到达目的地 B。
    - 还存在一种可能性：始终找不到“主机 B”（有可能该主机“断线 or 关机 or 根本不存在”）。为了避免数据包长时间在网络上闲逛，还需要引入某种【数据包存活机制】（洋文叫做“Time To Live”，简称 TTL）。
  - 通常会采用某个整数（TTL 计数）表示数据包能活多久。当主机 A 发出这个数据包的时候，这个“TTL 计数”就已经设置好了。每当这个数据包被路由器转发一次，“TTL 记数”就减一。当 TTL 变为零，这个数据包就死了（被丢弃）。
- 网际互联 internetwork
- 不提供服务质量的承诺，只保证最大努力传输，不会对数据包进行编号，这样网络层设计比较简单
- 协议实现通常包含在操作系统自带的网络模块中
- 各种异构的网络在网络层看来好像是一个统一的网络，这种网络也称为IP网
- 有了IP网之后,主机之间通信无需看到异构的细节，网络的物理异构性对通信来讲是透明的。在这种覆盖全球的IP网上再使用TCP协议，构成现在的互联网

### Packets

![](../_static/packet_struct.png)

### Internet Protocol IP 协议

- IP 分片与重组
  - 对于IP，如果某个分片被弄丢了，那么在最终目的地是没办法正确重组的。整个IP包就是一个垃圾IP包，IP层也不会有重传机制
  - Linux在重组IP包时，现将所有的分片放到重组队列中，如果30秒中重组队列中的包没有到齐，则重组过程失败（意味着上层，比如TCP，将无法收到该IP包），重组队列被释放，同时向发送方以ICMP协议通知失败信息
  - 如果上层是TCP, 那么TCP会负责重传。可以看到， 分片会带来一些问题，所以TCP尽量避免分片，而采用提前分段的方式
  - IP不是可靠协议，没有提供一种数据未传达以后的处理机制，这被认为是上层协议TCP或UDP要做的事情
  - 每种数据链路的最大传输单元 MTU 都是不相同的，如 FDDI 数据链路 MTU 4352、以太网的 MTU 是 1500 字节等，每种数据链路的 MTU 之所以不同，是因为每个不同类型的数据链路的使用目的不同。使用目的不同，可承载的 MTU 也就不同
  - IP包理论上可以有64K字节这么大，但是以太网数据链路的MTU为1500字节，因此对于大于1500字节的IP包都需要进行分片发送,消息（或者其他数据）被分割为小的独立的包，并通过因特网在计算机之间传送
  - 当 IP 数据包大小大于 MTU 时， IP 数据包就会被分片,经过分片之后的 IP 数据报在被重组的时候，只能由目标主机进行，路由器是不会进行重组的。
  - 在分片传输中，一旦某个分片丢失，则会造成整个 IP 数据报作废，所以 TCP 引入了 MSS 也就是在 TCP 层进行分片不由 IP 层分片，那么对于 UDP 尽量不要发送一个大于 MTU 的数据报文
  - IP 数据包是在数据链路层处理的基础上对数据进行打包，不同数据链路的各自最大传输单位（MTU）不尽相同，但是 IP 协议又是可以实现多个数据链路之间通信的协议，所以，意味着它对不同的数据链路差异进行了抽象，使得上层无需关注底层网络构造细节
  - IP 协议采用对数据包进行分片处理，将较大的 IP 包分割成较小的包，到了接收端以后再根据分片序号重新组合起来传递给上一层，通过这种方式实现了对数据链路层的抽象
    - 分片会导致路由器处理负荷加重，所以只要允许，都不会让路由器进行 IP 数据包的分片处理
    - 在分片过程中，如果某个分片丢失，整个 IP 数据包都会作废。实际实现过程中，为了避免路由器对 IP 数据包进行分片，还产生了一种叫做「路径 MTU 发现」的技术，所谓路径 MTU 指的是从发送端主机到接收端主机之间路由器不需要对 IP 数据包进行分片的最大 MTU 的大小，然后发送端根据这个 MTU 的大小对数据包进行分片发送，从而避免路由器对其进行分片处理
- 不会占用两个正在通信的计算机之间的通信线路。降低了对网络线路的需求
- 每条线可以同时满足许多不同的计算机之间的通信需要
- 协议规定，在互联网中所有主机和路由器，必须能够接收长度不超过576字节的IP数据报，除非知道对方能够接受更大的数据量（比如通过TCP约定），即上层交来的512字节+最大60字节IP首部+4字节富余量
- IP 协议头
  - 八位TTL字段
    - 规定该数据包在穿过多少个路由之后才会被抛弃。某个IP数据包每穿过一个路由器，该数据包的TTL数值就会减少1，当该数据包的TTL成为零，它就会被自动抛弃
    - 最大值 255，也就是说一个协议包也就在路由器里面穿行255次就会被抛弃了，根据系统的不同，这个数字也不一样，一般是32或者是64
  - IP包中的“片偏移”以8个字节为偏移单位，也就是说IP包中的数据量必须为8个字节的整数倍
  - IP包中的“协议”字段表示该IP包中所包含数据所使用的上层协议，比如TCP、UDP等
  - "总长度"的字段，为16位，表示整个IP数据包的总长度（字节），从这个16为可以算出理论上IP包的长度最大为2^16=64k字节，但是现实中极少有这种包出现
  - 一个数据包在传输过程中，目的IP和源IP是永远不变的(使用了NAT协议除外)，一直是主机和服务器的IP，而目的mac和源mac却是一直变化的，这也是arp协议存在的一个理由
  - 三层(IP)广播即IP地址中的主机号全是1的IP包，IP广播将导致二层链路层广播（MAC目的地址全是F）。另外，IP地址为255.255.255.255的也是广播，这种情况用于主机还不知道自己IP地址的时候(比如向DHCP服务器索要地址时、PPPOE拨号时等)，由于路由器不会转发广播帧，因此这种广播也不会逃出本地网络

#### IPv4

- 由 32 位正整数来表示，在计算机是以二进制方式处理,以每 8 位为组，共分为 4 组，每组以「.」隔开
- IP地址：在IP层有一个类似的地址标识，格式：`{ <Network-number>, <Host-number> }`，分为网络位和地址位，可以减少路由器中路由表记录的数目
- net-number:ip 地址所在网络地址，就可以限定拥有相同网络地址的终端都在同一个范围内，那么路由表只需要维护一条这个网络地址的方向，就可以找到相应终端
- host-number：ip 地址所在网络中主机号
- 广播:用于在同一个链路中相互连接的主机之间发送数据包
  - 广播地址:主机地址部分全部设置为1,表示该网络的广播地址
  - 本地广播:在本网络内广播。例如网络地址为 192.168.0.0/24 的情况下，广播地址是 192.168.0.255 。因为这个广播地址的 IP 包会被路由器屏蔽，所以不会到达 192.168.0.0/24 以外的其他链路上
    - 会被路由器屏蔽，不会到达外部网络
  - 直接广播:在不同网络之间的广播.例如网络地址为 192.168.0.0/24 的主机向 192.168.1.255/24 的目标地址发送 IP 包。收到这个包的路由器，将数据转发给192.168.1.0/24，从而使得所有 192.168.1.1~192.168.1.254 的主机都能收到这个包（由于直接广播有一定的安全问题，多数情况下会在路由器上设置为不转发）
  - 受限的广播地址为255.255.255.255。该地址用于主机配置过程中IP数据报的目的地址，在任何情况下，router不转发目的地址为255.255.255.255的数据报，这样的数据报仅出现在本地网络中。
  - 指向网络的广播 指向网络的广播地址是主机号为全1的地址。A类网络广播地址为netid.255.255.255，其中netid为A类网络的网络号。一个router必须转发指向网络的广播，但它也必须有一个不进行转发的选择。
  - 指向子网的广播 指向子网的广播地址为主机号为全1且有特定子网号的地址。作为子网直接广播地址的IP地址需要了解子网的掩码。例如，router收到128.1.2.255的数据报，当B类网路128.1的子网掩码为255.255.255.0时，该地址就是指向子网的广播地址；但是如果子网掩码为255.255.254.0，该地址就不是指向子网的广播地址。
  - 指向所有子网的广播 指向所有子网的广播也需要了解目的网络的子网掩码，以便与指向网络的广播地址区分开来。指向所有子网的广播地址的子网号和主机号为全1.例如，如果子网掩码为255.255.255.0，那么128.1.255.255就是一个指向所有子网的广播地址。
  - 路由器不转发广播包
- 多播|组播，使用D类地址，D类地址分配的28bit均用作多播组号而不再表示其他
  - 多播组地址包括1110的最高4bit和多播组号。它们通常可以表示为点分十进制数，范围从224.0.0.0到239.255.255.255。
  - 多播的出现减少了对应用不感兴趣主机的处理负荷。
  - 特点：
    - 允许一个或多个发送者（组播源）发送单一的数据包到多个接收者（一次的，同时的）的网络技术
    - 可以大大的节省网络带宽，因为无论有多少个目标地址，在整个网络的任何一条链路上只传送单一的数据包
    - 多播技术的核心就是针对如何节约网络资源的前提下保证服务质量
- 网络
  - 一个网络表示所有IP网络号相同的主机的集合
  - 实际上IP地址是标识一台主机（或路由器）和一条链路的接口。当一台主机同时连接两个网络是，那么这台主机就必须同时拥有两个IP，比如路由器就是典型的例子
  - 主机为全部为0的IP地址表示本网络
  - 在同一个局域网中主机和路由器的IP地址和MAC地址之间的映射问题
  - 局域网内部需要数据链路层进行通信，而不同的局域网之间（互联网其实就是将多个不同的局域网连接起来实现互联）需要借助网络层才能通信，完整的计算机网络需要借助这两个分层才能最终完成通信
- 分离网络号和主机号
  - 两台计算机要通讯，首先要判断是否处于同一个广播域内，即网络地址是否相同
  - 如果网络地址相同，表明接受方在本网络上，那么可以把数据包直接发送到目标主机
  - 路由器寻址工作中，也就是通过这样的方式来找到对应的网络号，进而把数据包转发给对应的网络内

#### 子网

- 子网划分只是一种逻辑上的划分方式，子网与广播域之间并不存在一一对应的关系
- 一个VLAN上也可以运行多个子网，只是通常情况下在实施时将子网与VLAN一一对应了
- VLAN通过帧的tag为标记帧是属于哪个VLAN的，广播帧不会在VLAN之间传播，泛洪也只会传播到自己所属的VLAN中
- 子网划分之后，所有子网对外依然是一个逻辑上的单一网络，也即外界通过一次路由便可以找到
- 子网掩码决定一个子网的计算机数目,主机个数,看主机号位数 2^n-2,有两个特殊IP
  - 主机号全为 1:指定某个网络下所有主机，用于广播
  - 主机号全为 0:指定某个网络
- 子网掩码
  - TCP/IP协议使用子网掩码确定主机是在本地子网中还是在远程网络中。将Ip地址和子网掩码(subnet mask)排在一起比较，就可以分清楚改地址的网络部分和主机部分
  - 表示子网络特征的一个参数。在形式上类似IP地址，也是一个32位二进制数字，它的网络部分全部为1，主机部分全部为0，将两个IP地址与子网掩码分别进行 AND 运算，然后比较结果是否相同，如果是的话，就表明它们在同一个子网络中，否则就不是。
  - 将 IP 地址与子网掩码做按位与运算，就可以计算出该 IP 地址的网络地址部分
  - 网络部分都为1，主机部分都为0，目的判断ip的网络部分，如255.255.255.0(11111111.11111111.11111111.00000000)
    - 将子网掩码和 IP 地址按位计算 AND，得到网络号
  - 划分子网：将主机地址分为两个部分：子网网络地址和子网主机地址
    - 从 8 位主机号中借用 2 位作为子网号
    - 子网地址就有 4 个，分别是 00、01、10、11
- 早期开发阶段，子网是通过 IP 地址最左侧的 8 位划分子网，这种方式只允许划分 256 个网络

#### IPv6

- 128 位，每 16 位作为一组，每组用冒号 「:」 隔开，如果出现连续的 0 时还可以将这些 0 省略，并用两个冒号 「::」隔开。但是，一个 IP 地址中只允许出现一次两个连续的冒号
- 在设计时没有考虑与 IPv4 的兼容性问题
- 类型
- 单播地址，用于一对一的通信
  - 在同一链路单播通信，不经过路由器，可以使用链路本地单播地址，IPv4 没有此类型
  - 在内网里单播通信，可以使用唯一本地地址，相当于 IPv4 的私有 IP
  - 在互联网通信，可以使用全局单播地址，相当于 IPv4 的公有 IP
- 组播地址，用于一对多的通信
  - D 类地址，也即组播地址，使用这个地址，可以将包组播给一批机器。
  - 当一台机器上的某个进程想监听某个组播地址的时候，需要发送 IGMP 包，所在网络的路由器就能收到这个包，知道有个机器上有个进程在监听这个组播地址。
  - 当路由器收到这个组播地址的时候，会将包转发给这台机器，这样就实现了跨路由器的组播。
- 任播地址，用于通信最近的节点，最近的节点是由路由协议决定
- 没有广播地址
- IPv6 相比 IPv4 的首部改进
- 取消了首部校验和字段。 因为在数据链路层和传输层都会校验，因此 IPv6 直接取消了 IP 的校验。
- 取消了分片/重新组装相关字段。 分片与重组是耗时的过程，IPv6 不允许在中间路由器进行分片与重组，这种操作只能在源与目标主机，这将大大提高了路由器转发的速度。
- 取消选项字段。 选项字段不再是标准 IP 首部的一部分了，但它并没有消失，而是可能出现在 IPv6 首部中的「下一个首部」指出的位置上。删除该选项字段是的 IPv6 的首部成为固定长度的 40 字节
- 优点
- 可自动配置，即使没有 DHCP 服务器也可以实现自动分配IP地址，真是便捷到即插即用啊。
- 包头包首部长度采用固定的值 40 字节，去掉了包头校验和，简化了首部结构，减轻了路由器负荷，大大提高了传输的性能。
- 有应对伪造 IP 地址的网络安全功能以及防止线路窃听的功能，大大提升了安全性
- [IPv6 测试聚合站](https://ipv6.stream/)
- IP vs MAC
  - MAC 的作用则是实现「直连」的两个设备之间通信，而 IP 则负责在「没有直连」的两个网络之间进行通信传输。
  - 源IP地址和目标IP地址在传输过程中是不会变化的，只有源 MAC 地址和目标 MAC 一直在变化
- 参考
  - [IP 基础知识“全家桶”](https://mp.weixin.qq.com/s/4Gwxm1DAj3nAdqHPRdEuLA)

```sh
apt-get  install bridge-utils

brctl addbr br0
sudo brctl show [br0]

brctl delbr br1

brctl addif br0 eth0
brctl delif br0 eth0
```

### 分类网络架构 Classful Network Architecture

- 在 1981 年提出，原始 IP划分方式，在1993年提出的无分类编址之后，虽然在教科书中依然可以看到分类 IP，但是事实上基本不用了
- A 类地址 以 0 开头，第 1-8 位是网络地址，后24位是主机地址
  - 网络地址个数（2^7-2）0.0.0.0~127.0.0.0
  - 默认子网掩码/8，即 255.0.0.0
  - 容纳主机地址 16777214（2^24-2）1.0.0.0~127.255.255.255
  - 私有 IP 10.0.0.0-10.255.255.255
  - 0.0.0.0 已经不是一个真正意义上的 IP 地址了。表示一个所有不清楚的主机和目的网络集合
    - 不清楚 指在本机的路由表里没有特定条目指明如何到达。作为缺省路由
- B 类地址 以 10 开头，第 1-16 位是网络地址，后 16 位是主机地址
  - 网络地址个数（2^14-1） 128.0.0.0~191.255.255.255
  - 默认子网掩码/16，即255.255.0.0
  - 可容纳主机地址 65534 (2^16-2)
  - 私有 IP 172.16.0.0-172.131.255.255
- C 类地址 前三位以 110 开头，第 1-24 位是网络地址，后 8 位是主机地址
  - 网络地址个数（2^21-1） 192.0.0.0~223.255.255.255
  - 默认子网掩码/24，即255.255.255.0
  - 可容纳主机地址 254 (2^8-2)
  - 私有 IP  192.168.0.0-192.168.255.255
- D 类和 E 类地址是没有主机号的，不可用于主机 IP
- D 类地址：前四位以 1110 开头，第 1-32 位是网络地址 224.0.0.0~239.255.255.255，没有主机地址
  - 广播无法穿透路由，若想给其他网段发送同样的包可以使用多播
  - 用于多播(multicast)，将包发送给特定组内的所有主机
  - 224.0.0.0 ~ 224.0.0.255 预留组播地址，只能局域网中，路由器是不会进行转发的
  - 224.0.1.0 ~ 238.255.255.255 用户可用组播地址，可以用于 Internet 上
    - 224.0.0.1  IRDP（internet路由发现，使用组播功能）组播地址
  - 239.0.0.0 ~ 239.255.255.255 本地管理组播地址，可供内部网在内部使用，仅在特定的本地范围内有效
- E 类：240.0.0.0-255.255.255.255(其中255.255.255.255为全网广播地址)
  - 前四位是1111，保留为以后使用
  - 一般用于研究用途
- 根据头部是否为1的标志位，判断类型，找出网络地址和主机地址
- 缺点
  - 同一网络下没有地址层次
  - A、B、C类有个尴尬处境，就是不能很好的与现实网络匹配
- 特殊
  - {0,0}:网络号和主机号都全部为0，表示“本网络上的本主机”，只能用作源地址
  - {0，host-id}:本网络上的某台主机。 只能用作源地址
  - {-1,-1}：表示网络号和主机号的所有位上都是1（二进制），用于本网络上的广播，只能用作目的地址，发到该地址的数据包不能转发到源地址所在网络之外
  - {net-id,-1}:直接广播到指定的网络上。 只能用作目的地址
  - {net-id,subnet-id,-1}:直接广播到指定网络的指定子网络上。 只用作目的地址
  - {net-id,-1,-1}:直接广播到指定网络的所有子网络上。 只能用作目的地址
  - {127，}:即网络号为127的任意ip地址。 都是内部主机回环地址(loopback),永远都不能出现在主机外部的网络中
- 环回地址
  - 在同一台计算机上的程序之间进行网络通信时所使用的一个默认地址
  - 使用一个特殊的 IP 地址 127.0.0.1 作为环回地址，与该地址具有相同意义的是一个叫做 localhost 的主机名
  - 使用这个 IP 或主机名时，数据包不会流向网络
  - 在同一台计算机内部的程序之间进行网络通信时所使用的默认地址，一般使用一个特殊的 IP 地址 127.0.0.1 作为环回地址，该地址还有一个与之具有相同意义的主机名 localhost，使用这个 IP 地址或主机名，数据包不会流向网络。
- 127.0.0.1 vs 0.0.0.0
  - 属于特殊地址。都属于A类地址。都是IPV4地址
  - 0.0.0.0 用于表示一个无效的，未知的或者不可用的目标
    - 在服务器中，0.0.0.0指的是本机上的所有IPV4地址，如果一个主机有两个IP地址，192.168.1.1 和 10.1.2.1，并且该主机上的一个服务监听的地址是0.0.0.0,那么通过两个ip地址都能够访问该服务
    - 在路由中，0.0.0.0表示的是默认路由，即当路由表中没有找到完全匹配的路由的时候所对应的路由
  - 所有网络号为 127 地址都被称之为回环地址(所有发往该类地址的数据包都应该被 loop back)
    - 回环测试：使用 `ping 127.0.0.1` 测试某台机器上的网络设备，操作系统或者TCP/IP实现是否工作正常
    - DDos攻击防御：网站收到DDos攻击之后，将域名A记录到127.0.0.1，即让攻击者自己攻击自己
    - 大部分Web容器测试的时候绑定的本机地址
  - localhost:一个域名，用于指代this computer或者this host,可以用它来获取运行在本机上的网络服务

### 无类别域间路由 Classless Inter-Domain Routing CIDR

- 判断是不是本地局域网
- IETF 在 1993 年提出替代分类网络架构，CIDR 基于可变长子网掩码（Variable-length Subnet Masking、VLSM）
- 缓解互联网中路由器中转发表的增长速度
- 缓解 IPv4 地址耗尽的速度
- A.B.C.D/N 32 比特的 IP 地址被划分为两部分，前面是网络号，后面是主机号，使用可变长度的子网掩码来划分地址块,N 表示网络号长度，范围 0 ~ 32
- 10.100.122.2/24
  - 广播地址 10.100.122.255。如果发送这个地址，所有 10.100.122 网络里面的机器都可以收到。
  - 子网掩码 255.255.255.0
- 网络号 将子网掩码和 IP 地址按位计算 AND
- 回收不再使用的 IP 资源并投入再利用
- 私有 IP 地址:允许组织内部的 IT 人员自己管理、自己分配，而且可以重复
- 公有 IP 地址
  - 由 ICANN (互联网名称与数字地址分配机构) 组织统一分配管理
  - IANA 是 ICANN 的其中一个机构，它负责分配互联网 IP 地址，是按州的方式层层分配
    - ARIN 北美地区
    - LACNIC 拉丁美洲和一些加勒比群岛
    - RIPE NCC 欧洲、中东和中亚
    - AfriNIC 非洲地区
    - APNIC 亚太地区
- 整个网络里面的第一个地址 192.168.0.1，往往就是私有网络的出口地址

![CIDR](../_static/cidr_example.jpg "CIDR")

### 网络结构

- 自治系统 AS Autonomous System
  - Stub AS：对外只有一个连接。这类 AS 不会传输其他 AS 的包。例如，个人或者小公司的网络。
  - Multihomed AS：可能有多个连接连到其他的 AS，但是大多拒绝帮其他的 AS 传输包。例如一些大公司的网络。
  - Transit AS：有多个连接连到其他的 AS，并且可以帮助其他的 AS 传输包。例如主干网。
- 每个自治系统都有边界路由器，通过它和外面的世界建立联系

### 网关

- 在跨网关访问的时候，牵扯到 MAC 地址和 IP 地址的变化
- 通过CIDR 和子网掩码 判断同一个网段
  - 同一个网段：直接将源地址和目标地址放入 IP 头中，然后通过 ARP 获得 MAC 地址，将源 MAC 和目的 MAC 放入 MAC 头中
  - 不是同一网段：需要发往默认网关 Gateway。Gateway 的地址一定是和源 IP 地址是一个网段的。往往不是第一个，就是第二个。
  - 通过 ARP 获得网关的 MAC 地址，将源 MAC 和网关的 MAC 放入 MAC 头中，发送出去

#### 转发网关

- 不改变 IP 地址
- 通过目标 IP，不断驱动到不同网段，通过ARP 获取目标 MAC地址
- 源 MAC 与 目的 MAC 在不同子网段内跳转
  - 前一跳目的 MAC 为下一跳的源 MAC 一致
  - 但是需要表示为不同的网卡MAC

#### 网络地址转换 Network Address Translation NAT

- 改变 IP 地址
- 要配置公网地址 [whatismyip](https://www.whatismyip.com/)
- 脱离私有网段，要转化为公网地址
- 进入私有网段，转化为私网地址
- 在 IP 数据包通过路由器时修改网络地址的技术，能够将当前地址空间中的 IP 地址映射到另一个地址空间.
  - 当数据包从内部访问外部网络时，NAT 会为当前请求分配一个端口、覆写数据包中的源地址和端口并将地址和端口信息存储到本地的转换表中
  - 当数据包从外部进入网络内部时，NAT 会根据数据包的 IP 地址和端口号查找到私有网络中对应的主机和端口号并覆写数据包中的目的地址和端口
- 本身是有带上端口号,端口号在路由器B上有一个NAT映射, 路由器知道123端口代表着内网主机192.188.1.101:321,
- 网络地址与端口转换 NAPT：把 IP 地址 + 端口号一起进行转换
  - 两个私有 IP 地址都转换 IP 地址为公有地址 120.229.175.121，但是以不同的端口号作为区分
  - 生成一个 NAPT 路由器的转换表，就可以正确地转换地址跟端口的组合，令客户端 A、B 能同时与服务器之间进行通信
  - 这种转换表在 NAT 路由器上自动生成
  - 争议：
    - NAT 使用端口号是用于进程寻址的，而不是用于主机寻址的
    - NAT 路由器作为第三层（网络层）的设备，应当只处理达到网络层的分组
    - NAT 违反了主机应当直接彼此对话的原则
  - 问题
    - 外部无法主动与 NAT 内部服务器建立连接，因为 NAPT 转换表没有转换记录。
    - 转换表的生产与转换操作都会产生性能开销
    - 通信过程中，如果 NAT 路由器重启了，所有的 TCP 连接都将被重置
  - 一个被称为 “conntrack” 的 netfilter 系统可以识别已有连接的回复报文。每个连接都在 conntrack 系统中有自己的 NAT 状态。反向转换是自动完成的。
    - 允许针对某个报文检查其处理方式以及该报文匹配规则集合中的哪条规则。
    - 为了使用这项特殊的功能，可在合适的位置插入“跟踪规则”。这些规则会选择被跟踪的报文。假设一个来自 IP 地址 C 的主机正在访问一个 IP 地址是 S 以及端口是 P 的服务。想知道报文匹配了哪条 NAT 转换规则，系统检查了哪些规则，以及报文是否在哪里被丢弃了。
    - 要处理的是传入连接，所以将规则添加到 prerouting 钩子上。prerouting 意味着内核尚未决定将报文发往何处。修改目标地址通常会使报文被系统转发，而不是由主机自身处理。
- Nat有session
- 解决
  - IPv6 可用范围非常大，以至于每台设备都可以配置一个公有 IP 地址
  - NAT 穿越技术拥有这样的功能，能够让网络应用程序主动发现自己位于 NAT 设备之后，并且会主动获得 NAT 设备的公有 IP，并为自己建立端口映射条目，注意这些都是 NAT设备后的应用程序自动完成的,在 NAT 穿越技术中，NAT 设备后的应用程序处于主动地位，它已经明确地知道 NAT 设备要修改它外发的数据包，于是它主动配合 NAT 设备的操作，主动地建立好映射，这样就不像以前由 NAT 设备来建立映射了

![NAPT](../_static/napt.jpg "NAPT")

### 路由控制

- IP 地址:用来识别计算机网路中互连主机和路由器
- 「跳」是网络中的一个区间（网段），IP 数据包正是在网络中一个个跳之间转发，因此 IP 路由也叫多跳路由，在每一个区间内决定着包在下一跳被转发的路径。
- 路由控制表：所有主机和路由器都维护着一张路由控制表，该表记录 IP 数据在下一步应该发给哪个路由器，IP 数据包将根据这个路由表在各个数据链路上传输。
  - 每一条规则至少包含这三项信息 目的网络 出口设备 下一跳网关
- 策略路由：除了可以根据目的 ip 地址配置路由外，还可以根据源 IP 地址、入口设备、TOS多个参数来配置路由。举例：
  - 家里有两个租户,IP 地址为 192.168.1.101/24 和 192.168.1.102/24，网关192.168.1.1/24
  - 运营商 1 给路由器分配的地址是 183.134.189.34/32，而运营商网络里面的网关是 183.134.188.1/32。
  - 运营商 2 给路由器分配的地址是 60.190.27.190/30，运营商网络里面的网关是 60.190.27.189/30
  - 租户 A 不想多付钱，他说我就上上网页，从不看电影，凭什么收我同样贵的网费啊？

```sh
# 路由规则：去 10.176.48.0/20 目标网络，从 eth0 端口出去，经过 10.173.32.1
ip route add 10.176.48.0/20 via 10.173.32.1 dev eth0

# 根据 源IP 配置路由表
ip rule add from 192.168.1.0/24 table 10 
ip rule add from 192.168.2.0/24 table 20

# 一条路由规则中，也可以走多条路径
ip route add default scope global nexthop via 100.100.100.1 weight 1 nexthop via 200.200.200.1 weight 2


ip route list table main 

60.190.27.189/30 dev eth3  proto kernel  scope link  src 60.190.27.190
183.134.188.1 dev eth2  proto kernel  scope link  src 183.134.189.34
192.168.1.0/24 dev eth1  proto kernel  scope link  src 192.168.1.1
127.0.0.0/8 dev lo  scope link
default via 183.134.188.1 dev eth2

# 添加一个 名字叫 chao 的 Table
# 从 192.168.1.101 来的包都查看个 chao 这个新的路由表
echo 200 chao >> /etc/iproute2/rt_tables
ip rule add from 192.168.1.101 table chao

ip rule ls
0:  from all lookup local 
32765:  from 192.168.1.101ggg lookup chao
32766:  from all lookup main 
32767:  from all lookup default

# 在 chao 路由表中添加规则 默认的路由走慢的
ip route add default via  60.190.27.189 dev eth3 table chao
ip route flush cache
```

#### 静态路由

- 在路由器上，配置一条一条规则

#### 动态路由控制

- 路由器根据与其他路由器相互交换信息时自动刷新
- 为让动态路由及时刷新路由控制表，在网络上互连的路由器之间必须设置好路由协议，保证正常读取路由控制信息
- 在发送 IP 包时，首先要确定 IP 包首部中的目标地址，再从路由控制表中找到与该地址具有相同网络地址的记录，根据该记录将 IP 包转发给相应的下一个路由器。
- 如果路由控制表中存在多条相同网络地址的记录，就选择相同位数最多的网络地址，也就是最长匹配
- 主机 A 要发送一个 IP 包，其源地址是 10.1.1.30 和目标地址是 10.1.2.10，由于没有在主机 A 的路由表找到与目标地址 10.1.2.10 的网络地址，于是把包被转发到默认路由（路由器 1 ）
- 路由器 1 收到 IP 包后，也在路由器 1 的路由表匹配与目标地址相同的网络地址记录，发现匹配到了，于是就把 IP 数据包转发到了 10.1.0.2 这台路由器 2
- 路由器 2 收到后，同样对比自身的路由表，发现匹配到了，于是把 IP 包从路由器 2 的 10.1.2.1 这个接口出去，最终经过交换机把 IP 数据包转发到了目标主机

##### 动态路由算法

- 距离矢量路由（distance vector routing）基于 Bellman-Ford 算法的。
  - 每个路由器都保存一个路由表，包含多行，每行对应网络中的一个路由器，每一行包含两部分信息，一个是要到目标路由器，从那条线出去，另一个是到目标路由器的距离。每个路由器都是知道全局信息的
  - 更新：每个路由器都知道自己和邻居之间的距离，每过几秒，每个路由器都将自己所知的到达所有的路由器的距离告知邻居，每个路由器也能从邻居那里得到相似的信息。
  - 每个路由器根据新收集的信息，计算和其他路由器的距离
  - 比较简单，但是还是有问题
    - 好消息传得快，坏消息传得慢。
      - 如果有个路由器加入了这个网络，它的邻居就能很快发现它，然后将消息广播出去。要不了多久，整个网络就都知道了。
      - 一旦一个路由器挂了，挂的消息是没有广播的。当每个路由器发现原来的道路到不了这个路由器的时候，感觉不到它已经挂了，而是试图通过其他的路径访问，直到试过了所有的路径，才发现这个路由器是真的挂了。直连路由通过间连路由获取挂掉路由信息，不断增加距离，直到超过某一阈值
    - 每次发送的时候，要发送整个全局路由表
  - 最早路由协议 RIP 就是这个算法。适用于小型网络（小于 15 跳）。当网络规模都小的时候，没有问题。现在一个数据中心内部路由器数目就很多，因而不适用了
- 链路状态路由（link state routing），基于 Dijkstra 算法
  - 当一个路由器启动的时候，首先是发现邻居，向邻居 say hello，邻居都回复。然后计算和邻居的距离，发送一个 echo，要求马上返回，除以二就是距离。
  - 然后将自己和邻居之间的链路状态包广播出去，发送到整个网络的每个路由器。这样每个路由器都能够收到它和邻居之间的关系的信息。因而，每个路由器都能在自己本地构建一个完整的图，然后针对这个图使用 Dijkstra 算法，找到两点之间的最短路径。
  - 不像距离距离矢量路由协议那样，更新时发送整个路由表。链路状态路由协议只广播更新的或改变的网络拓扑，这使得更新信息更小，节省了带宽和 CPU 利用率。
  - 一旦一个路由器挂了，它的邻居都会广播这个消息，可以使得坏消息迅速收敛。

##### OSPF Open Shortest Path First 开放式最短路径优

- 一个基于链路状态路由协议，广泛应用在数据中心中的协议。由于主要用在数据中心内部，用于路由决策，因而称为内部网关协议（Interior Gateway Protocol  IGP）
- 基于UDP
- 通过路由器之间通告网络接口的状态来建立链路状态数据库，生成最短路径树，OSPF会自动计算路由接口上的Cost值，也可以通过手工指定该接口的Cost值，手工指定的优先于自动计算的值。
- OSPF 计算 Cost，同样是和接口带宽成反比，带宽越高，Cost值越小。
- 等价路由： 到达目标相同Cost值的路径，可以执行负载均衡，最多6条链路同时执行负载均衡。

##### BGP Border Gateway Protocol 边界网关协议

- 运行于 TCP 上的一种自治系统的路由协议
- 自治系统间，边界路由器之间使用 eBGP 广播路由。
- 内部网络也需要访问其他的自治系统。边界路由器如何将 BGP 学习到的路由导入到内部网络呢？就是通过运行 iBGP，使得内部的路由器能够找到到达外网目的地的最好的边界路由器。
- 一种外部网关协议（Exterior Gateway Protocol，EGP），与OSPF、RIP等内部网关协议（Interior Gateway Protocol，IGP）不同，BGP不在于发现和计算路由，而在于控制路由的传播和选择最佳路由
- 使用TCP作为其传输层协议（端口号179），提高协议的可靠性
- 路径矢量路由协议（path-vector protocol）距离矢量路由协议的升级版。
  - 除了下一跳 hop 之外，还包括了自治系统 AS 的路径，从而可以避免坏消息传得慢的问题
  - 也即上面所描述的，B 知道 C 原来能够到达 A，是因为通过自己，一旦自己都到达不了 A 了，就不用假设 C 还能到达 A 了。
- 支持CIDR（Classless Inter-Domain Routing，无类别域间路由）
- 路由更新时，BGP只发送更新的路由，大大减少了BGP传播路由所占用的带宽，适用于在Internet上传播大量的路由信息
- BGP路由通过携带AS路径信息彻底解决路由环路问题
- BGP提供了丰富的路由策略，能够对路由实现灵活的过滤和选择
- BGP易于扩展，能够适应网络新的发展

### ICMP Internet Control Message Protocol 因特网消息控制协议

- 当某个网关发现传输错误时，立即向信源主机发送ICMP报文，报告出错信息，让信源主机采取相应处理措施，它是一种差错和控制报文协议，不仅用于传输差错报文，还传输控制报文。
- 报文是封装在 IP 包里面的
- 类型
  - 查询报文类型  主动请求 8 ICMP ECHO REQUEST
  - 主动请求应答 0 ICMP ECHO REPLY
  - 差错报文类型 通知出错原因的错误消息
    - 终点不可达 3
      - 网络不可达代码为 0
      - 主机不可达代码 1
      - 协议不可达代码 2
      - 端口不可达代码为 3
      - 需要进行分片但设置了不分片位代码 4
    - 源抑制 4 让源站放慢发送速度
    - 超时 11 超过网络包的生存时间还是没到
    - 重定向 5
    - 不发ICMP差错报文
      - ICMP 的差错报文出错
      - 目的地址为广播时
      - 源地址不唯一时也不发差错报文
- 确认 IP 包是否成功送达目标地址
- 在 IP 通信中如果某个 IP 包因为某种原因未能达到目标地址，那么这个具体的原因将由 ICMP 负责通知报告发送过程中 IP 包被废弃的原因和改善网络设置等
- dpkt定义包packet类，网络报文类型的基础类. IP，ICMP等继承于dpkt class，每一个子类有一个`_hdr_` 结构，此结构定义了不同报文的头部，方便取出相应的控制字段

#### ping

- verify connectivity between you and a remote system
- 网路连通性探测:确定网络是否正确连接，以及网络连接的状况
- 实现长时间的网络监控
- 基于 ICMP 协议工作的，是TCP/IP协议的一部分。利用ping命令可以检查网络是否连通，可以很好地帮助分析和判定网络故障
- 比起原生的 ICMP，多了两个字段
  - 标识符 区分目标
  - 序号 用于区分连续 ping 的时候发出的多个数据包。每发出一个请求数据包，顺序号会自动加 1。
  - 为能够计算往返时间 RTT，会在报文的数据部分插入发送时间
- 结构相对复杂一些。除了前面还是 IP，ICMP 的前 8 字节不变，后面则跟上出错的那个 IP 包的 IP 头和 IP 正文的前 8 个字节
- 下面代码为实例
  - 支持 pipe
- 参数
  - -c: 执行 ping 操作的次数, 默认是一直执行, 除非被中断
  - -D 显时间戳
  - -i: 每次执行 ping 操作的间隔时间, 默认是 1s
    - [-l] :定义所发送数据包的大小，默认为32字节
    - [-n] :定义所发数据包的次数
  - -s: 指定执行 ping 操作时发送的包的大小, 默认是 56B, 添加报文头之后, 最终发送的是 64B
    - [-t] :表示不间断向目标IP发送数据包
- 使用 fflush()，不然文件不会有信息，因为 awk 有缓存
- pingpong:一种数据缓存的手段，通过 pingpong 操作可以提高数据传输的效率
  - 什么时候需要 pingpong？在两个模块间交换数据时，上一级处理的结果不能马上被下一级所处理完成，这样上一级必须等待下一级处理完成才可以送新的数据，这样就会对性能产生很大的损失。
  - 引入 pingpong 后我们可以不去等待下一级处理结束，而是将结果保存在 pong 路的缓存中，pong 路的数据准备好的时刻，ping 路的数据也处理完毕（下一级），然后无需等待直接处理 pong 路数据，上一级也无需等待，转而将结果存储在 ping 路。这样便提高了处理效率。
- 很多中间设备都是禁止 ping 的，但是 ping 不通不代表网络不通。这个时候就要使用 telnet，通过其他协议来测试网络是否通
- [gping](https://github.com/orf/gping) Ping, but with a graph

![ping 发送和接收过程](../_stataic/ping_flow.png)

```sh
sudo tcpdump -i wlp2s0 icmp

00:48:12.034466 IP 192.168.0.113 > 101.37.178.161: ICMP echo request, id 3, seq 1, length 64
00:48:12.048534 IP 101.37.178.161 > 192.168.0.113: ICMP echo reply, id 3, seq 1, length 64

00:48:13.036797 IP 192.168.0.113 > 101.37.178.161: ICMP echo request, id 3, seq 2, length 64
00:48:13.408808 IP 101.37.178.161 > 192.168.0.113: ICMP echo reply, id 3, seq 2, length 64

00:48:14.037651 IP 192.168.0.113 > 101.37.178.161: ICMP echo request, id 3, seq 3, length 64
00:48:14.210610 IP 101.37.178.161 > 192.168.0.113: ICMP echo reply, id 3, seq 3, length 64

00:48:15.038701 IP 192.168.0.113 > 101.37.178.161: ICMP echo request, id 3, seq 4, length 64
00:48:16.059451 IP 192.168.0.113 > 101.37.178.161: ICMP echo request, id 3, seq 5, length 64
00:48:16.080487 IP 101.37.178.161 > 192.168.0.113: ICMP echo reply, id 3, seq 4, length 64
00:48:16.080560 IP 101.37.178.161 > 192.168.0.113: ICMP echo reply, id 3, seq 5, length 64

10 packets captured
10 packets received by filter
0 packets dropped by kernel

ping zhibo8.cc
PING zhibo8.cc (101.37.178.161) 56(84) bytes of data.
64 bytes from 101.37.178.161 (101.37.178.161): icmp_seq=1 ttl=90 time=14.1 ms
64 bytes from 101.37.178.161 (101.37.178.161): icmp_seq=2 ttl=90 time=372 ms
64 bytes from 101.37.178.161 (101.37.178.161): icmp_seq=3 ttl=90 time=173 ms
64 bytes from 101.37.178.161 (101.37.178.161): icmp_seq=4 ttl=90 time=1042 ms
64 bytes from 101.37.178.161 (101.37.178.161): icmp_seq=5 ttl=90 time=21.2 ms
--- zhibo8.cc ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4025ms
rtt min/avg/max/mdev = 14.109/324.432/1041.832/381.612 ms, pipe 2
```

```sh
# local host是系统网络保留名，是127.0.0.1的别名，每台计算机都应该能够将该名字转换成该地址。
# 否则，则表示主机文件（/Windows/host）中存在问题。
ping localhost
ping6 example.com

# 如果测试成功，表明网卡、TCP/IP协议的安装、IP地址、子网掩码的设置正常
# 如果测试不成功，表示TCP/IP的安装或设置存在有问题，表示本地配置或安装存在问题，应当对网络设备和通讯介质进行测试、检查并排除。
ping 127.0.0.1

# 如果测试成功，表明本地网络中的网卡和载体运行正确
# 如果收到0个回送应答，那么表示子网掩码不正确或网卡配置错误或电缆系统有问题。
ping 局域网内其他IP

# 如果应答正确，表示局域网中的网关路由器正在运行并能够做出应答。
ping 网关IP

# 如果收到正确应答，表示成功的使用了缺省网关。对于拨号上网用户则表示能够成功的访问Internet（但不排除ISP的DNS会有问题）
ping 远程IP

## 对域名执行，必须先将域名转换成IP地址，通常是通过DNS服务器
# 出现故障，则表示本机DNS服务器的IP地址配置不正确，或它所访问的DNS服务器有故障
# 能正常运行，那么计算机进行本地和远程通信基本上就没有问题
#
# 命令的成功并不表示所有的网络配置都没有问题，例如，某些子网掩码错误就可能无法用这些方法检测到
ping www.yahoo.com

ping baidu.com | awk '{ print strftime("%Y.%m.%d %H:%M:%S",systime())"\t"$0; fflush() }'
ping baidu.com | awk '{"date" | getline date; print date,$0}'
ping baidu.com | awk -v date="$(date +"%Y-%m-%d %r")" '{print date, $0}'

# 未加 fflush()，执行命令生成文件会等一会才会有信息打印到文件里
nohup ping baidu.com | awk '{ print strftime("%Y-%m-%d %H:%M:%S",systime())"\t" $0; fflush() }' >> long_ping.txt &

nohup ping baidu.com -i 1 | while read pong; do echo "$(date +"%Y-%m-%d %H:%M:%S") | $pong"; done | tee -a ping-baidu.com.log &
```

#### Traceroute

- trace the path from one system to another, including routers in between 侦测主机到目的主机之间所经路由情况的重要工具
- 故意设置特殊 TTL，来追踪去往目的地时沿途经过的路由器。
  - Traceroute 参数指向某个目的 IP 地址，会发送一个 UDP 数据包。
  - 将 TTL 设置成 1，也就是说一旦遇到一个路由器或者一个关卡，就表示它“牺牲”了。自动把TTL减1，而TTL变为0以后，路由器就把这个包给抛弃了，并同时产生一个主机不可达的ICMP数据报给主机。类型是时间超时
  - 接下来，将 TTL 设置为 2。第一关过了，第二关就“牺牲”了，那就知道第二关有多远。
  - 如此反复，直到到达目的主机。这样，Traceroute 就拿到了所有的路由器 IP。当然，有的路由器压根不会回这个 ICMP。这也是 Traceroute 一个公网的地址，看不到中间路由的原因
  - 怎么知道 UDP 有没有到达目的主机呢？
    - Traceroute 程序会发送一份 UDP 数据报给目的主机，但它会选择一个不可能的值作为 UDP 端口号（大于 30000）。
    - 当该数据报到达时，将使目的主机的 UDP 模块产生一份“端口不可达”错误 ICMP 报文。
    - 如果数据报没有到达，则可能是超时。
- 故意设置不分片，从而确定路径的 MTU。
  - 首先是发送分组，并设置“不分片”标志。发送的第一个分组的长度正好与出口 MTU 相等。
  - 如果中间遇到窄的关口会被卡住，会发送 ICMP 网络差错包，类型为“需要进行分片但设置了不分片位”。其实，这是故意的，每次收到 ICMP“不能分片”差错时就减小分组的长度，直到到达目标主机。
- tracerouter发udp，为啥出错回icmp？
  - 正常情况下，协议栈能正常走到udp，当然正常返回udp。
  - 主机不可达，是 ip 层的（还没到udp）。ip层，当然只知道回icmp。报文分片错误也是同理

```sh
traceroute google.com
```

#### mtr

### IGMP

- 因特网组管理协议，工作在主机（组播成员）和最后一跳路由之间
- IGMP 报文向路由器申请加入和退出组播组，默认情况下路由器是不会转发组播包到连接中的主机，除非主机通过 IGMP 加入到组播组，主机申请加入到组播组时，路由器就会记录 IGMP 路由器表，路由器后续就会转发该组播地址的数据包了。
- IGMP 报文采用 IP 封装，IP 头部的协议号为 2，而且 TTL 字段值通常 为 1，因为 IGMP 是工作在主机与连接的路由器之间
- IGMPv2
  - 路由器会周期性发送目的地址为 224.0.0.1（表示同一网段内所有主机和路由器） IGMP 常规查询报文；
  - 主机1 和 主机 3 收到这个查询，随后会启动「报告延迟计时器」，计时器的时间是随机的，通常是 0~10 秒，计时器超时后主机就会发送 IGMP 成员关系报告报文（源 IP 地址为自己主机的 IP 地址，目的 IP 地址为组播地址）。如果在定时器超时之前，收到同一个组内的其他主机发送的成员关系报告报文，则自己不再发送，这样可以减少网络中多余的 IGMP 报文数量；
  - 路由器收到主机的成员关系报告报文后，就会在 IGMP 路由表中加入该组播组，后续网络中一旦该组播地址的数据到达路由器，它会把数据包转发出去
- 离开组播组工作机制
  - 网段中仍有该组播组
    - 主机 1 要离开组 224.1.1.1，发送 IGMPv2 离组报文，报文的目的地址是 224.0.0.2（表示发向网段内的所有路由器）；
    - 路由器收到该报文后，以 1 秒为间隔连续发送 IGMP 特定组查询报文（共计发送 2 个），以便确认该网络是否还有 224.1.1.1 组的其他成员；
    - 主机 3 仍然是组 224.1.1.1 的成员，因此它立即响应这个特定组查询。路由器知道该网络中仍然存在该组播组的成员，于是继续向该网络转发 224.1.1.1 的组播数据包
  - 网段中没有该组播组
    - 主机 1 要离开组播组 224.1.1.1，发送 IGMP 离组报文；
    - 路由器收到该报文后，以 1 秒为间隔连续发送 IGMP 特定组查询报文（共计发送 2 个）。此时在该网段内，组 224.1.1.1 已经没有其他成员了，因此没有主机响应这个查询；
    - 一定时间后，路由器认为该网段中已经没有 224.1.1.1 组播组成员了，将不会再向这个网段转发该组播地址的数据包

### 路由器 Router

- 连接因特网中各局域网、广域网的设备。在路由器中记录着路由表，会解析目标IP地址，根据信道的情况自动选择和设定路由，以最佳路径，按前后顺序发送信号
- 路由器每一个端口，都有独立 MAC 地址，而且同时还能把数据包做一次转发
- 所有 LAN 网口相当于其内部通过一个交换机相连接，交换机再连接到路由器的LAN 端网卡上
  - LAN 只有一个网卡，一个地址加交换机的形式
- 路由器每一个接口都有不同的网络号，因此一个路由器的接口就连接的一个网络
- 路由器隔离丢弃广播帧
- 通常来说，路由器中也有默认路由记录，当路由表中找不到目的IP的路由记录时使用默认路由
- 能够连接不同类型的局域网和广域网，如以太网、ATM网、FDDI网、令牌环网等。不同类型的网络，其传送的数据单元——帧（Frame）的格式和大小是不同的

#### router vs 网关

- 路由器是一台设备，有五个网口或者网卡，相当于有五只手，分别连着五个局域网。
- 每只手 IP 地址都和局域网 IP 地址相同的网段，每只手都是它握住的那个局域网的网关。
- 任何一个想发往其他局域网的包，都会到达其中一只手，被拿进来，拿下 MAC 头和 IP 头，看看，根据自己的路由算法，选择另一只手，加上 IP 头和 MAC 头，然后扔出去。

### 3层交换机 Layer 3 switching

- 与路由器的差别在于——“3层交换机”链接的几个子网是【同种】网络；而路由器可以连接【异种】网络。

### AP

- 用于无线网络的交换机，用来接入无线终端，是无线网络中的核心设备

## Data Link 数据链路层

- 信息打包：把“比特流”打包成更大的一坨，以方便更上层的协议进行处理
- 差错控制
  - 物理介质传输，可能受到环境的影响。不仅仅体现为“噪声”，有时候会出现严重的干扰，导致物理层传输的“比特流”出错（某个比特“从0变1”或“从1变0”）
  - 可靠传输: 在出错率很低的链路上很少用，但是无线链路WLAN会保证可靠传输
  - 需要负责检查物理层的传输是否出错
  - “检错算法”只能检测出错误
    - 差错检测(CRC) 对传输的数据计算出一个【校验值】，接收方收到数据会重新计算校验和，如果算出来不对，就把收到的数据丢弃，让对方重发。
  - “纠错算法”不但能检测出错误，还能纠正错误
- 流量控制
  - 假设两个端点通过同一个物理信道进行通讯，这两个端点处理信息的速度可能不同。
  - 如果发送方输出信息的速度超过接收方处理信息的速度，通讯就会出问题。于是就需要有某种机制来协调，确保发送方的发送速度不会超出接收方的处理速度。
- 透明传输:零比特填充、转义字符
- 同一个冲突域下的所有主机，同一时刻都只允许一台机器发送数据。
- “网卡硬件 ＆ 网卡驱动”会包含链路层协议的实现

### Media Access Control  MAC

- controls how a computer on the network gains access to the data and permission to transmit it.
- 确保对下层物理介质的使用，不会出现冲突
- 信道划分
- 轮流协议
- 随机接入协议
  - 以太网采用

### Logical Link Control  LLC

- controls frame synchronization, flow control and error checking.

#### 最大传输单元 MTU

- 指的是链路层数据区,不包括链路层的首部和尾部的18个字节
- 以太网规定正文部分不允许超过 1500 个字节。正文里面有 IP 的头、TCP 的头、HTTP 的头。是网络层IP数据报的长度限制
  - MTU 1500表示二层MAC帧大小不超过1518,MAC 头14 字节，尾4字节
- IP数据报的首部为20字节，所以IP数据报的数据区长度最大为1480字
  - IP数据报大于1500字节，发送方IP层需要分片（fragmentation）
- 1480字节用来放TCP传来的TCP报文段或UDP传来的UDP数据报的
  - UDP数据报首部8字节，UDP数据报的数据区最大长度 1472字节
  - IP分片过程看起来透明的，对于TCP协议来说，**但有一个缺陷：即使只丢失一片数据也要重新传整个数据报**
  - 当来自TCP报文段的某一片丢失后，TCP在超时后会重发整个TCP报文段，该报文段对应于一份IP数据报（而不是一个分片），没有办法只重传数据报中的一个数据分片。
  - 由于UDP的特性，当某一片数据传送中丢失时。接收方将无法重组报文，故而导致整个UDP报文的丢弃。因此，在局域网环境下，一般建议将UDP数据包控制在1472byte以下为宜
- 假定MTU为1500来发送数据，而途经某个网络的MTU值小于1500字节，系统将会使用一系列的机制来调整MTU值，使数据报能够顺利到达目的地，这样就会做许多不必要的操作。鉴于Internet上的标准MTU值为576字节，建议在进行Internet的UDP编程时，将UDP的数据长度控件在576-8-20=548字节以内

#### qdisc  queueing discipline 排队规则

- 内核如果需要通过某个网络接口发送数据包，都需要按照为这个接口配置的 qdisc（排队规则）把数据包加入队列。

##### pfifo

- 不对进入的数据包做任何的处理，数据包采用先入先出的方式通过队列。

##### pfifo_fast

- 稍微复杂一些，队列包括三个波段（band）。在每个波段里面，使用先进先出规则。
- 三个波段（band）的优先级也不相同。band 0 的优先级最高，band 2 的最低。如果 band 0 里面有数据包，系统就不会处理 band 1 里面的数据包，band 1 和 band 2 之间也是一样。
- 数据包按照服务类型（Type of Service，TOS）被分配到三个波段（band）里面的。TOS 是 IP 头里面的一个字段，代表了当前的包是高优先级的，还是低优先级的。

### 帧 frame

- 封装成帧: 把网络层数据报加头和尾
- 帧头
  - 源 MAC地址
  - 目的 MAC地址 数据包在链路上广播，MAC 的网卡才能发现，这个包是给它的。MAC 的网卡把包收进来，然后打开 IP 包，发现 IP 地址也是自己的，再打开 TCP 包，发现端口是自己
- 类型：IP 里面包含 TCP、UDP，以及 HTTP
- CRC 循环冗余检测
  - 通过 XOR 异或算法，来计算整个包是否在发送的过程中出现错误

| 目标 MAC  | 源 MAC   | 类型      | 数据            | CRC     |
| ------- | ------- | ------- | ------------- | ------- |
| 6 bytes | 6 bytes | 2 bytes | 46～1500 bytes | 4 bytes |

### MAC 地址

- 为每一个端点引入【惟一的】标识
- 定义网卡和网卡唯一的mac地址，全球唯一，用来识别同一链路中的不同计算机
- 6个字节
- 前三个字节 OUI 由IEEE统一分配，由商家购买
- 后三个字节有商家自行分配
- 前6位厂商编号
- 后6位网卡流水号
- 以太网规定接入网络的所有终端都应该具有网卡接口，数据包必须是从一个网卡的mac地址到另一网卡接口的mac地址
- 一个网络包要从一个地方传到另一个地方，除了要有确定的 MAC 地址，还需要有定位功能。IP 地址，才是有远程定位功能的
- MAC 地址更像是身份证，是一个唯一的标识。它的唯一性设计是为了组网的时候，不同的网卡放在一个网络里面的时候，可以不用担心冲突。从硬件角度，保证不同的网卡有不同的标识。
  - 有一定定位功能的，只不过范围非常有限
  - 通信范围比较小，局限在一个子网里面

### ARP Address Resolution Protocol

- 根据 IP 地址获取MAC地址的一种解析协议
- 只有是一个网段的调用，才会发送 ARP 请求，获取 MAC 地址
- 如果是一个跨网段的调用，Linux 默认的逻辑不会直接将包发送到网络上，而是企图将包发送到网关
- 本来主机是完全不知道 IP 对应的是哪个主机的哪个接口，当主机要发送一个IP包的时候，会首先查一下 ARP 高速缓存（就是一个IP-MAC地址对应表缓存）
- 如果查询 IP－MAC值对不存在，借助 ARP 请求与 ARP 响应两种类型的包确定 MAC 地址
  - 主机向网络发送一个ARP协议广播包，里面有待查询IP地址，而接收到这份广播的包的所有主机都会查询自己的IP地址
  - 当同个链路中的所有设备收到 ARP 请求时，会去拆开 ARP 请求包里的内容，如果 ARP 请求包中的目标 IP 地址与自己的 IP 地址一致，那么设备就将自己 MAC 地址塞入 ARP 响应包返回给 ARP 广播主机
  - 广播主机拿到ARP包后会更新自己的ARP缓存（就是存放IP-MAC对应表的地方）。
  - 发送广播的主机就会用新的ARP缓存数据准备好数据链路层的的数据包发送工作
- 操作系统通常会把第一次通过 ARP 获取的 MAC 地址缓存起来，以便下次直接从缓存中找到对应 IP 地址的 MAC 地址
- 代理 ARP工作原理：路由器可以分割网段和广播，比如广播后只能在同一个网段接收到，而在其他的网段不会听见广播
- 多个交换机
  - 比如数据包经过交换机A到达交换机B，交换机B又将包复制为多份广播出去。
  - 如果整个局域网存在一个环路，使得数据包又重新回到了最开始的交换机A，这个包又会被A再次复制多份广播出去。
  - 如此循环，数据包会不停得转发，而且越来越多，最终占满带宽，或者使解析协议的硬件过载，行成广播风暴。

### RARP Reverse Address Resolution Protocol

- 已知 MAC 地址求 IP 地址
- 通常这需要架设一台 RARP 服务器，在这个服务器上注册设备的 MAC 地址及其 IP 地址。然后再将这个设备接入到网络，接着：
  - 该设备会发送一条「我的 MAC 地址是XXXX，请告诉我，我的IP地址应该是什么」的请求信息。
  - RARP 服务器接到这个消息后返回「MAC地址为 XXXX 的设备，IP地址为 XXXX」的信息给这个设备。
  - 设备就根据从 RARP 服务器所收到的应答信息设置自己的 IP 地址
- 无盘工作站，即没有硬盘的机器，无法持久化ip地址到本地，但有网卡，所以可以用RARP协议来获取IP地址。
- 可以用于局域网管理员想指定机器IP（与机器绑定，不可变），又不想每台机器去设置静态IP的情况，可以在RARP服务器上配置MAC和IP对应的ARP表，不过获取每台机器的MAC地址，好像也挺麻烦的。这个协议现在应该用得不多了吧，都用BOOTP或者DHCP了。

### 交换机|网络交换机 network switch|2层交换机

- 工作在2层（链路层）设备，能够理解链路层协议
- 在没有查到地址表记录时，则向所有端口广播（泛洪）该帧，请注意这里的广播并不是是广播帧的一是，而只是一种动作。
- 如果交换机某端口接收到了广播帧，则不会查MAC地址表，而是直接将该帧发给所有的其他端口。
- 具备自动寻址能力和交换作用，由于交换机根据所传递信息包的目的地址，将每一信息包独立地从源端口送至目的端口，避免了和其他端口发生碰撞
- 换机某端口连接的主机想和另一个端口连接的主机通信，交换机就会通过转发表发送那个端口，不可能去其他端口，不存在发错端口.交换机每一个端口都是一个冲突域，也就是说交换机可以隔离冲突域
- 在划分vlan的前提下可以实现多个广播域，每个接口都是一个单独的冲突域
- 本职工作内网交换，在大型网络寻路中还是要通过路由器来实现；同样的，路由器的工作是不同网络之间的寻路，请不要将路由器作为交换机使用，尤其是终端较多的情况下。随着网络的发展，也出现三层交换机来承载部分内网寻路的工作。
- 拥有一条高带宽的背部总线和内部交换矩阵。交换机的所有的端口都挂接在这条背部总线上，当控制电路收到数据包以后，处理端口会查找内存中的地址对照表以确定目的MAC地址应该从哪个端口发出，通过内部交换矩阵迅速将数据包传送到目的端口。目的MAC地址若不存在，交换机才广播到所有的端口，接收端口回应后交换机会“学习”新的地址，并把它添加入内部地址表中。
- MAC 地址表|转发表 MAC 地址学习能力
  - 交换机内部维护一张 MAC 地址表，记录着每一个 MAC 地址的设备，连接在其哪一个端口上
  - 最开始 MAC 地址表是空的
  - 根据每次接受的包，以接受包数据，记录源 MAC 与端口对应关系
  - 经过网络中机器不断地通信，交换机最终将 MAC 地址表建立完毕
  - 数据到达交换机时，交换机内部通过维护的 MAC 地址表，发现目标机器 B 的 MAC 地址 映射到了端口 1 上，于是把数据从 1 号端口发给目标设备
- 交换机互联
  - 随着机器数量越多，交换机的端口也不够。
  - 一台交换机的某一个端口映射另外一台交换机的所有端口
- 给这台设备加入一个指令，可以根据网口名称自动寻址传输数据。实现任意两台电脑间的互联
  - 保存每个计算机的网卡MAC地址与所在计算机的接口：通过学习，可以把MAC地址，端口号完善
  - 既可以连接PC机，又可以连接路由器
  - 根据Mac地址表转发数据
  - mac地址表含有Mac地址和接口
- 支持生成树算法。可以构建出物理有环，逻辑无环的网络，网络冗余和数据传输效率都甩Hub好几条街。SW是目前组网的基本设备之一
- 在划分vlan的前提下可以实现多个广播域，每个接口都是一个单独的冲突域

### 网桥/桥接器 network bridge

- 让两台不同网络类型的电脑相连
  - 虚拟机 bridge 模式: Guest OS 的虚拟网卡，对于 Host OS 所在的外部网络是可见的
- 根据Mac地址的信息转发到网桥的不同端口上
- 二层虚拟网络设备，把若干个网络接口“连接”起来，使得网口之间报文可以转发
- 通过对比目的地MAC与网桥内部的地址表来判断帧是否送往另一个端口。
- 能够解析收发的报文，读取目标Mac地址信息，和自己Mac地址表结合，来决策报文转发的目标网口
- 会学习源Mac地址。在转发报文时，网桥只需要向特定的端口转发，从而避免不必要的网络交互
- 如果遇到了一个从未学过的地址，就无法知道这个报文应该向哪个网口转发，就将报文广播给除了报文来源之外的所有网口
- 对学习到的Mac地址表加上超时时间，默认5min。如果网桥收到了对应端口MAC地址回发的包。则重置超时时间，否则过了超时时间后，就认为哪个设备不在那个端口上了，他就会广播重发
- 广播发送数据
  - 向本网络内的所有设备发送数据包，对比接收者mac地址，不是丢包，是接受

### 局域网 LAN

### 环路问题

- 两个交换机将两个局域网同时连接起来的时候

#### STP  Spanning Tree Protocol

- 生成树:有环的图中的环破了
- 拓扑设备分类
  - Root Bridge 根交换机,可以比喻为“掌门”交换机，是某棵树的老大，是掌门，最大的大哥
  - Designated Bridges 指定交换机
    - 可以想像成一个“小弟”，对于树来说，就是一棵树的树枝
    - 所谓“指定”的意思是，我拜谁做大哥，其他交换机通过这个交换机到达根交换机，也就相当于拜他做了大哥
    - 这里注意是树枝，不是叶子，因为叶子往往是主机
- Bridge Protocol Data Units （BPDU）网桥协议数据单元
  - 可以比喻为“相互比较实力”的协议。
  - 当两个交换机碰见的时候，也就是相连的时候，就需要互相比一比内力了。
  - BPDU 只有掌门能发，已经隶属于某个掌门的交换机只能传达掌门的指示。
- Priority Vector，优先级向量。可以比喻为实力 （值越小越牛）
  - 实力是一组 ID 数目，`[Root Bridge ID, Root Path Cost, Bridge ID, and Port ID]`
  - 为什么这样设计呢？这是因为要看怎么来比实力。
    - 先看 Root Bridge ID。拿出老大的 ID 看看，发现掌门一样，那就是师兄弟，可以比
    - 再比 Root Path Cost，也即距离老大距离，看同一个门派内谁和老大关系铁；
    - 最后比 Bridge ID，比我自己的 ID，拿自己的本事比。
- 流程
  - 每个设备有管理员初始分配的优先级
  - 设备间互相发送 BPDU 比较，级别低的接受高的发送的 Priority Vector
    - Root Bridge 合并
    - Designated Bridges 与 Root Bridge 优化路径，选最短路径
    - Designated Bridges 存在环，路径唯一化
    - Designated Bridges 与 其它 Root Bridge 相遇  Root Bridge 之间对比，合并

### 以太网 Ethernet

- Use the tcp_nopush directive together with the sendfile on;directive. This enables NGINX to send HTTP response headers in one packet right after the chunk of data has been obtained by sendfile().
- 默认路由：A default route is the route that takes effect when no other route is available for an IP destination address.If a packet is received on a routing device, the device first checks to see if the IP destination address is on one of the device’s local subnets. If the destination address is not local, the device checks its routing table. If the remote destination subnet is not listed in the routing table, the packet is forwarded to the next hop toward the destination using the default route. The default route generally has a next-hop address of another routing device, which performs the same process. The process repeats until a packet is delivered to the destination.
- 以太网中一台机器发送的数据所有机器都能接收到，然后基于目的地MAC判断是否接收该数据
- 当以太网中计算机发现有CRC检查出错时，直接丢弃该包。数据的可靠性传输交给了TCP这样的高层协议。以太网保证最大努力交付，即不可靠交付。
- 以太网通过CSMA/CD保证同一时刻只有一台计算机在发送数据，并且是半双工，如果发现有碰撞，则推迟一个随机时间再次发送。
- 以太网采用曼彻斯特编码
- 10BASE-T双绞线以太网的出现，是局域网发展史的重要里程碑，从此以太网拓扑有总线型变为星型，而以太网在局域网中占据了统治地位。
- 使用了集线器的以太网在逻辑上依然是个总线网，依然采用CSMA/CD协议。
- 以太网一开始是总线型的，是因为那时的以太网交换机太昂贵了，而无源的总线结构要廉价得多。
- 以太网各帧之间的发送有一定间隙，因此帧不需要结束定界符。
- 虽然以太网交换机不适用CSMA/CD，但是其数据帧依然使用以太网帧，因此依然叫以太网
- 以太网（Ethernet）数据帧的长度必须在46-1500字节之间，这是由以太网的物理特性决定的

### VLAN 虚拟局域网

- 虚拟隔离
- 在原来的二层的头上加一个 TAG，里面有一个 VLAN ID，一共 12 位，可以划分 4096 个 VLAN
- 支持 VLAN 的交换机，把二层的头取下来的时候，能够识别 VLAN ID。只有相同 VLAN 的包，才会互相转发，不同 VLAN 的包，是看不到的。这样广播问题和安全问题就都能够解决了
- 设置交换机每个口所属的 VLAN
- 每个 VLAN 口都是可以重新设置的
- 交换机之间通过Trunk 口连接：可以转发属于任何 VLAN 的口

### iproute2 vs net-tools

- net-tools 
	  - 起源于 BSD，自 2001 年起，Linux 社区已经停止对其进行维护
	  - 通过 procfs(/proc) 和 ioctl 系统调用去访问和改变内核网络配置
- iproute2 
	- iproute2 旨在取代 net-tools，并提供一些新功能
	- route2 虽然取代意图很明显，但是这么多年过去了，net-tool依然还在被广泛使用
	- 一些Linux发行版已经停止支持net-tools，只支持iproute2
	- iproute2则通过netlink套接字接口与内核通讯。
- net-tools中工具的名字比较杂乱，而iproute2则相对整齐和直观，基本是ip命令加后面的子命令
- ip|ipconfig|ifconofig
  - 有 IP 地址的 eth0 网卡 scope： global 网卡可以对外接收来自各个地方的包
  - lo loopback 环回接口 scope： host 网卡仅仅可以供本机相互通信，经过内核处理后直接返回，不会在任何网络中出现
  - net_device flags 网络设备的状态标识 <BROADCAST,MULTICAST,UP,LOWER_UP>
    - UP 表示网卡处于启动的状态
    - BROADCAST 表示这个网卡有广播地址，可以发送广播包
    - MULTICAST 表示网卡可以发送多播包
    - LOWER_UP 表示 L1 是启动的，也即网线插着呢
    - MTU1500  最大传输单元 MTU 为 1500，这是以太网的默认值

| function                       | net-tool | iproute2         |
|:------------------------------ |:-------- |:---------------- |
| Address and link configuration | ifconfig | ip addr, ip link |
| Routing tables                 | route    | ip route         |
| Neighbors                      | arp      | ip neigh         |
| Tunnels                        | iptunnel | ip tunnel        |
| Multicast                      | ipmaddr  | ip maddr         |
| Statistics                     | netstat  | ss               |

```sh
## work with the network cards
ip link
# Display status of all network cards (up/down) and also their Mac address
ip link show 
# Change the status of network card eth0
ip link set eth0 down|up 

# work with the IP addresses set (or to be set) on the network adapters
ip address show

# 手动分配 IP 地址
sudo ip address add 169.254.0.1 dev eth0
# Add to eth1 the address 192.168.0.23
# can add a secondary address
ip addr add 192.168.0.23/24 brd + dev eth1

ip a l wlp2s0

## routing tables
ip route
# Show the default routing table.
ip route show

## ## Dynamic policy routing
# connected to 3 different network:
# – Public router – net 120.120.120.0/24 GW 120.120.120.1
# – DMZ area – net 192.168.0.0/24 GW 192.168.0.1
#  Internal network – net 10.0.0.0/24 GW 10.0.0.1
ip route add table 2 default via 10.0.0.1
ip route add table 3 default via 192.168.0.1

ip rule add from 10.0.0.0/24 table 2
ip rule add from 192.168.0.0/24 table 3

ip route show table X 
ip route flush table X

# 查看交互邻居
ip neighbour

root@test:~# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00 # mac
    inet 127.0.0.1/8 scope host lo # 设备 
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether fa:16:3e:c7:79:75 brd ff:ff:ff:ff:ff:ff
    inet 10.100.122.2/24 brd 10.100.122.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::f816:3eff:fec7:7975/64 scope link 
       valid_lft forever preferred_lft forever

ipconfig # 显示每个已经配置了的接口的IP地址、子网掩码和缺省网关值
ipconfig /all # 为DNS和WINS服务器显示它已配置且所有使用的附加信息，并且能够显示内置于本地网卡中的物理地址（MAC）
```

## 物理层 Phsycal Layer

- 数据 比特流（Bits）
- 负责0、1比特流与物理设备电压高低、光的闪灭之间的互换
- 物理介质把电脑连接起来的物理手段，决定了电信号(0和1)的传输方式，物理介质的不同决定了电信号的传输带宽、速率、传输距离以及抗干扰性等等
- 信噪比（Signal-to-noise ratio）：总是会存在某些环境干扰，称之为“噪声”（Noise）。“信道传输的有用信息”与“无用的干扰噪声”，这两者的比值
  - 单位 分贝 “decibel
- 带宽：受限于某些基本的物理学定律（比如“光速上限”）以及会有或多或少的环境干扰（噪声）
  - 由于物理层是最底下的一层，物理层之上的其它层次总是要直接或间接地依赖【物理信道】。因此，其它层次建立的“逻辑信道”，其带宽只会比“物理信道”的最大带宽更小。换句话说：“物理信道”的带宽上限也就是整个协议栈的带宽上限。
- 多路复用（Multiplexing）
  - 频分多路复用/FDM（Frequency-Division Multiplexing）根据频率拆分。不同的线路占用不同的频段，互不干扰。（电台广播用的就是这个思路）
    - 缺点
      - 要依赖足够宽的频段（频段是稀缺资源）；
      - 不同线路的流量可能会动态变化。如果某个线路空闲，其占用的频段就浪费了。
    - （注：光纤通讯中有个“波分多路复用/WDM”，本质上就是 FDM）
  - 时分多路复用/TDM（Time-Division Multiplexing）这种思路只用一个很窄的频段。为了在同一个频道发送多个信道，采用【分时机制】，把时间切割成很小的时间片，每个线路占用一个时间片。周而往复。
    - 有点像十字路口的红绿灯——每隔一段时间，其中一条路可以通行。
    - 优点：可以只使用一个很窄的频段。缺点是：线路越多，每条线路等待越久；即使某个线路空闲，依然会占用时间片（浪费了资源）
  - 码分多路复用/CDM（Code-Division Multiplexing）
    - 采用某种【编码】的技巧，使得多个端点可以在同一个时间点使用同一频段发送数据；由于他们采用不同的编码方式，不会相互干扰。
    - CDM 要依赖于“扩频技术”（spread spectrum），需占用一个比较宽的频道范围。这算是缺点
    - 优点
    - 可以支持 N 个线路（N 动态变化）；
    - 即使任何一个线路的流量动态变化，也不会浪费物理信道的资源。
    - 显然，这种思路明显优于 FDM ＆ TDM。如今在移动通讯领域大名鼎鼎的 ,CDMA（码分多址），采用的就是这个思路。

### 同轴电缆

- 用于早期以太网，传输速度通常在 10Mbps 以内。当然粗缆是可以到 1-2Gbps 的速度，不过现在几乎被我们接下来要说到的网线给取代了。

### 网线｜双绞线

- 市面上网线通常为八芯双绞线，传输距离建议不超过一百米。
- 常见的网线标准有五类线、超五类线、六类线、超六类线和七类线这五种标准。不同标准传输速率不同，但是都不建议超过 100 米。
- 水晶头要做交叉线，用的就是所谓的 1－3、2－6 交叉接法。
  - 水晶头的第 1、2 和第 3、6 脚，它们分别起着收、发信号的作用。
  - 将一端的 1 号和 3 号线、2 号和 6 号线互换一下位置，就能够在物理层实现一端发送的信号，另一端能收到。
- 网卡能自适应直连线

### 光导纤维 光纤

- 通常由玻璃或塑料制成，最外层会涂一层隔绝光线的材料。可以实现每秒万兆位的数据传送，传输距离可达数百公里
- 单模光纤传输距离长，可达 20-120 公里的距离。
- 多模光纤适用于低速短距离的场景，比如说一个局域网里的交换机之间的互联，交换机和路由器之间的互联都可以用多模光纤，传输距离在 2 公里以内。
- [submarine cable map](https://www.submarinecablemap.com/)

### 电磁波

- 作为对有线网络的扩展，电磁波的范围很广，适合作为信号传输的只有介于 3 Hz 和约 300 GHz 之间的无线电波，无线电波又被称为射频电波
- 无线网络就是用的无线电波中超高频的一部分。国内最常用的频段是 2.4 GHz 和 5 GHz

```sh
curl -w "TCP handshake: %{time_connect}s, SSL handshake: %{time_appconnect}s\n" -so /dev/null https://www.gemini.com
```

### IEEE 802.11 （Wi-Fi）

- 高质量无线 LAN.是 WECA（无线以太网兼容性联盟）为普及 IEEE802.11 的各种标准而打造的一个品牌
- 从 02 年开始更名为 Wi-Fi Appliance，该组织向 Wi-Fi 设备厂商提供 IEEE802.11 产品的互操性测试，并对合格的产品颁发 Wi-Fi Certified认证，因此，带有 Wi-Fi 标志的无线 LAN 设备意味着该产品已经过互操性测试并通过认证

### 网卡

- 包含了物理层的协议实现
- 在收到数据帧时通过硬件判断该帧的目的MAC地址是否发往本站，如果不是则丢弃。以下三种情况下表示帧是发往本站的：
  - 单播，即帧目的MAC地址=本机MAC地址
  - 多播，发送给该局域网上一部分机器
  - 广播，发送给局域网上所有的机器，MAC地址全是F
- 网卡可以设置为混杂模式，即不是发往本机的帧也可以接下来，比如有些抓包软件便是以这种方式工作的
- 网关要和当前的网络至少一个网卡是同一个网段的
- 因此手动配置一台机器的网络 IP 时，一定要好好问问网络管理员。如果在机房里面，要去网络管理员那里申请分配一段正确的 IP 地址。当然，真正配置的时候，一定不是直接用命令配置的，而是放在一个配置文件里面。不同系统的配置文件格式不同，但是无非就是 CIDR、子网掩码、广播地址和网关地址。
- 冲突域：一块网卡发送信息时有可能和另一块网卡冲突的所有的网卡的集合
- 广播域：一块网卡发出一个广播，能收到这个广播的所有的网卡的集合
- 一般来说一个网段就是一个冲突域，一个局域网就是一个广播域

```sh
# net-tools：
sudo ifconfig eth1 10.0.0.1/24
sudo ifconfig eth1 up

# iproute2
sudo ip addr add 10.0.0.1/24 dev eth1
sudo ip link set up eth1
```

### 调制解调器（modem）

- 把电脑要发送的“字节流”（数字信号）翻译成“模拟信号”，然后通过物理介质发送出去；当它从物理介质收到“模拟信号”，再翻译成“数字信号”，传回给电脑。

### 中继器 repeater

- 由于双绞线在传输信号时信号功率会逐渐衰减，当信号衰减到一定程度时将造成信号失真，因此在保证信号质量的前提下，双绞线的最大传输距离为100米。
- 当两台电脑之间的距离超过100米时，为了实现双机互 连，人们便在这两台电脑之间安装一个“中继器”，它的作用就是将已经衰减得不完整的信号经过整理，重新产生出完整的信号再继续传送。
- 放大器和中继器都是起放大信号的作用，只不过放大器放大的是模拟信号，中继器放大的是数字信号。

### 集线器 Hub

- 有多个口将多台电脑连接起来。和交换机不同，集线器没有大脑，完全在物理层工作，会将自己收到的每一个字节，都复制到其他端口上去（广播），不做任何处理
- 由于“经典以太网”的工作模式才“10兆”，所以集线器虽然低效，还能忍受
- “百兆以太网”发展成“交换式以太网”，用【交换机】代替“集线器”
- 发送数据包时，在头部拼接一个MAC 地址.目标设备根据头部的目标 MAC 地址信息，判断这个数据包的确是发给自己的收下，不是舍弃
- 一个将网线集结起来的作用，实现最初级的网络互通。集线器是通过网线直接传送数据的，工作在物理层
- 广播域
- 冲突域 集线器所有端口都属于一个冲突域
  - 集线器不能分割冲突域

### 本地互联

- 电脑用交叉线链接
- 两台电脑的 IP 地址、子网掩码和默认网关必须配置成为一个网络

## 网关 Gateway

- 互连网络中操作在OSI网络层之上的具有协议转换功能设施
- 互连
  - 异构型局域网，如互联专用交换网PBX与遵循IEEE802标准的局域网。 
  - 局域网与广域网的互联。 
  - 广域网与广域网的互联。 
  - 局域网与主机的互联（当主机的操作系统与网络操作系统不兼容时，可以通过网关连接）
- 分类
  - 协议网关：通常在使用不同协议的网络区域间做协议转换。
  - 应用网关：在使用不同数据格式间翻译数据的系统。
  - 安全网关：各种技术的融合，具有重要且独特的保护作用，其范围从协议级过滤到十分复杂的应用级过滤。

## 课程

- [TCP/IP 视频讲解 计算机网络](https://www.bilibili.com/video/av10610680)

## 图书

-  **《TCP/IP详解 卷1：协议 TCP/IP Illustrated, Volume 1: The Protocols》** Rechard Stevens
- 《TCP/IP高效编程：改善网络程序的44个技巧 Effective TCP/IP Programming 44 Tips to Improve Your Network Programs》
- 《UNIX 环境高级编程 Advanced Programming in the UNIX Environment》 apue
- 《UNIX 网络编程 Unix Network Programming》 unp
  - 《Unix Network Programming, Volume 1: The Sockets Networking API》  译者 杨继张
	- Sockets API的权威指南，但是网络编程远不是使用那十几个Sockets API那么简单 
  - 《UNIX Network Programming, Volume 2: Interprocess Communications》
- 《TCP/IP详解 卷2：实现》应用层开发的， 最多就写写socket的， 可以不用看第二部
  - 把 FreeBSD 中 TCP/IP 实现用几百页讲了个通透
  - 一步一步手把手的教写 TCP/IP 协议栈的实现,一个完整的C语言项目
- 《TCP/IP详解 卷3：TCP事务协议、HTTP、NNTP和UNIX域协议》
- The TCP/IP GUIDE
- 《TCP/IP 网络编程》
  - [net-lenrning-reference](https://github.com/chankeh/net-lenrning-reference):TCP/IP网络编程笔记
- 《Linux/UNIX 系统编程手册 The Linux Programming Interface: A Linux and UNIX System Programming Handbook》
- 《Unix/Linux 编程实践教程》 Bruce Molay
- 《Linux多线程服务器端编程》

## 参考

- [RFC793](http://tools.ietf.org/html/rfc793)
