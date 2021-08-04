## 后端|服务端开发

#backend

- 三高（高并发，高可用，高性能）
- 安全
- 存储
- 业务

## 方向

- 网络-分布式系统-并行计算
- 业务逻辑-WEB-游戏-交易-搜索
- 数据-CACHE-DB-KeyValue-文件存储服务
- 运维-负载均衡-容错-容灾-运维工具

## 职能

- web项目开发
- 底层API封装与开发:为前端操作提供服务
- 线上系统的优化
- 线上服务器的运维，常见问题的诊断与解决。
- 存储：文件 信息 信息之间的关系（数据库）

## 技能

- 掌握好语言基础
- 语言生态
  - apache+php 常用的PHP和apache模块
  - 框架：LN(A)MP架构
- 算法与数据结构
- 计算机网络
- 数据库
  - Mysql 优化、能创建高效的索引
  - nosql
- 消息中间件
- Linux与应用部署，Shell脚本
- 缓存
  - Memcache
  - Redis
- 服务化
- 项目扩展
  - restful
  - solr
- 模版引擎

## 业务

- 设计、实现相关业务服务
- 底层框架代码以及线上系统优化

## 进阶

- 了解大容量、高性能的分布式系统开发原理
- 在开放平台，分布式存储，分布式Cache

## 趋势

- 异步模式：Go Dubbo.异步非阻塞的 Nginx，而不是同步阻塞的 Apache。就是因为 Nginx 这样的异步程序，它的适应性更好、并发能力更强。现在在后端业务开发编程方面，技术力量强的团队已经开始将技术栈从同步模式切换为异步了。
  - 同步阻塞模式存在较多缺陷，并发能力弱、适应性差、慢速请求导致服务不可用。如：后台接口中调用第三方 API 的场景，同步模式效果极差。过去那些使用 Java、PHP、C++、Python、Ruby 语言开发的同步阻塞模式框架，用的人越来越少。
- Node.js:很少见到企业将 Node.js 作为公司后端方面的主要编程语言.
  - 异步回调的技术方案，以及在它之上所做的一些优化方案，包括 Promise、Future、Yield/Generator、Async/Await 等，改变了程序开发的风格和习惯。使用这些技术方案是无法兼容已有程序的
- 协程模式，兼顾了同步阻塞的可维护性和异步非阻塞的高并发能力。将会成为未来后端开发领域的主流技术方案。
  - 协程模式只需要对已有项目代码进行少量调整就可以运行起来，甚至可以完全兼容老项目。只需要框架层进行兼容即可。
  - GO 是最耀眼的那一个。协程、通道、静态语言、性能、富编译、标准库丰富、生态完整、Google 等
  - PHP + Swoole 的技术栈，更适合快速开发、快速迭代、业务驱动的场景。毕竟动态语言比静态语言还是要更加灵活、开发效率更高。而 Go 更适合编写系统级软件、核心业务。

## 系统性能

- 分类
  - Load Testing - 负载测试
  - Stress Testing - 压力测试
  - Soak Testing - 耐久测试
  - Spike Testing - 瞬压测试
- 指标
  - 技术指标
    - OK / KO
    - QPS / RPS / TPS
    - Response Time(min/max/mean/std/90%…)
    - Concurrent Users / Concurrent Requests
  - 业务指标
    - 平均同时在线用户数
    - 同时在线用户数
- 步骤
  - 确定性能需求（可选）
  - 准备测试环境和测试数据
  - 选择性能测试工具/平台，
  - 制定性能测试模型，编写性能测试代码
  - 运行性能测试
  - 分析测试报告
  - 性能调优 | 修复问题
- 测试核心
  - 网关(防火墙/VPN等)
  - 应用系统
  - 数据库
- 目标：核心三点都分别性能最优，并且全链路长时超高压能正常运行
- 内容
  - 架构易扩展
  - 测试较简单
  - 分析很困难
    - 性能测试结果 （ Throughput vs Latency 等）
    - 操作系统监控（ CPU, Memory, IO, Network 等）
    - 应用系统（ Profiler, Code Review 等）
    - 网关和数据库 （ Logs, CPU, Memory, IO 等）
  - 优化可灵活
    - 硬件基础设施优化
    - 操作系统优化
    - 应用系统优化
    - 数据库优化
    - 系统架构优化
  - 规划要按需
    - 选取测试指标
    - 建立测试模型
    - 变化测试指标
    - 分析测试报告、拟合测试数据

## 负载均衡 Load Balancer

- 当系统面临大量用户访问，负载过高的时候，使用服务器集群来提高网站的整体性能，一组计算机节点（或者一组进程）提供相同（同质的）服务，服务请求应该均匀分摊到这些节点上，使用集群和负载均衡提高整个系统的处理能力
- 把用户访问的流量通过「负载均衡器」根据某种转发策略，均匀的分发到后端多台服务器上，后端服务器可以独立响应和处理请求，从而实现分散负载的效果，负载均衡的关键在于将用户流量进行均衡减压的
- 让所有节点以最小代价、最好状态对外提供服务，这样系统吞吐量最大，性能更高，对于用户而言请求的时间也更小
- 在服务器集群中，需要有一台服务器充当调度者的角色，用户的所有请求都会首先由它接收，调度者再根据每台服务器的负载情况将请求分配给某一台后端服务器去处理。在这个过程中，调度者如何合理分配任务，保证所有后端服务器都将性能充分发挥，从而保持服务器集群的整体性能最优，这就是负载均衡要解决的问题。
- 类型
  - 二层负载均衡：基于MAC地址的二层负载均衡
  - 三层负载均衡：基于IP地址的负载均衡
  - 四层负载均衡：基于IP+端口的负载均衡
  - 七层负载均衡：基于URL等应用层信息的负载均衡
- 优点
  - 增强了系统可靠性
  - 提高了系统服务能力
  - 增强了应用可用性，最大化降低了单个节点过载、甚至crash概率
- 负载均衡是一种推模型，一定会选出一个服务节点，然后把请求推送过来
- 消息队列是拉模型：空闲服务节点主动去拉取请求进行处理，各个节点负载自然也是均衡的
  - 服务节点不会被大量请求冲垮，同时增加服务节点更加容易
  - 缺点：请求不是事实处理的

## IDC Internet Data Center 数据中心、机房

- 用来放置服务器。IDC网络是服务器间通信的桥梁
- 网络设备
  - 内网接入交换机：也称为TOR(top of rack),是服务器接入网络的设备。每台内网接入交换机下联40-48台服务器，使用一个掩码为/24的网段作为服务器内网网段。
  - 内网核心交换机：负责IDC内各内网接入交换机的流量转发及跨IDC流量转发。
  - MGW/NAT：MGW即LVS用来做负载均衡，NAT用于内网设备访问外网时做地址转换。
  - 外网核心路由器：通过静态互联运营商或BGP互联统一外网平台。

### 结构

每一个上游都均匀访问每一个下游，就能实现“将请求/数据【均匀】分摊到多个操作单元上执行

- 客户端层：典型调用方是浏览器browser或者手机应用APP，根据服务节点信息自行选择，然后将请求直接发送到选中服务节点
  - 知道服务器列表，要么是静态配置，要么有简单接口查询
  - backend server详细负载信息，就不适用通过客户端来查询
  - 算法要么是比较简单的，比如轮训（加权轮训）、随机（加权随机）、哈希这几种算法，只要每个客户端足够随机，按照大数定理，服务节点的负载也是均衡的
  - 较为复杂算法，比如根据backend的实际负载需要去额外的负载均衡服务（external load balancing service）查询到这些信息，在grpc中，就是使用这种办法
    - load balancer与grpc server通信，获得grpc server的负载等具体详细
    - grpc client从load balancer获取这些信息，最终grpc client直连到被选择的grpc server
- 反向代理层：系统入口，反向代理
  - 水平扩展通过“DNS轮询”实现的：dns-server对于一个域名配置了多个解析ip，每次DNS解析请求来访问dns-server，会轮询返回这些ip
  - 当nginx成为瓶颈的时候，只要增加服务器数量，新增nginx服务部署，增加一个外网ip，就能扩展反向代理层的性能，做到理论上的无限高并发
  - 请求轮询：和DNS轮询类似，请求依次路由到各个web-server；
  - 最少连接路由：哪个web-server的连接少，路由到哪个web-server；
  - ip哈希：按照访问用户的ip哈希值来路由web-server，只要用户的ip分布是均匀的，请求理论上也是均匀的，ip哈希均衡方法可以做到，同一个用户的请求固定落到同一台web-server上，此策略适合有状态服务，例如session；
- 站点应用层：实现核心应用逻辑，返回html或者json
  - 水平扩展通过“nginx”实现的。通过修改nginx.conf，设置多个web后端
  - 当web后端成为瓶颈的时候，增加服务器数量，新增web服务部署，在nginx配置中配置上新的web后端，就能扩展站点层的性能，做到理论上的无限高并发
- 服务层：如果实现了服务化，就有这一层
  - 水平扩展通过“服务连接池”实现的。站点层通过RPC-client调用下游的服务层RPC-server时，RPC-client中的连接池会建立与下游服务多个连接，当服务成为瓶颈的时候，只要增加服务器数量，新增服务部署，在RPC-client处建立新的下游服务连接，就能扩展服务层性能，做到理论上的无限高并发
  - 如果需要优雅进行服务层自动扩容，需要配置中心里服务自动发现功能的支持
- 缓存层：缓存加速访问存储
- 数据库层：数据库固化数据存储
- 在数据量很大情况下，数据层（缓存，数据库）涉及数据水平扩展，将原本存储在一台服务器上的数据（缓存，数据库）水平拆分到不同服务器上去，以达到扩充系统性能的目的，要考虑“数据的均衡”与“请求的均衡”两个点
  - 按照范围水平拆分：每一个数据服务，存储一定范围的数据，user0库，存储uid范围1-1kw，user1库，存储uid范围1kw-2kw
    - 规则简单，service只需判断一下uid范围就能路由到对应的存储服务；
    - 数据均衡性较好；
    - 比较容易扩展，可以随时加一个uid[2kw,3kw]的数据服务
    - 不足：请求的负载不一定均衡，一般来说，新注册的用户会比老用户更活跃，大range的服务请求压力会更大
  - 按照哈希水平拆分:每一个数据库，存储某个key值hash后的部分数据，user0库，存储偶数uid数据,user1库，存储奇数uid数据
    - 规则简单，service只需对uid进行hash能路由到对应的存储服务
    - 数据均衡性较好
    - 请求均匀性较好
    - 不容易扩展，扩展一个数据服务，hash方法改变时候，可能需要进行数据迁移
  - 水平拆分来扩充系统性能vs主从同步读写分离
    - 水平拆分扩展数据库性能：
      - 每个服务器上存储的数据量是总量的1/n，所以单机的性能也会有提升
      - n个服务器上的数据没有交集，那个服务器上数据的并集是数据的全集
      - 数据水平拆分到了n个服务器上，理论上读性能扩充了n倍，写性能也扩充了n倍（其实远不止n倍，因为单机的数据量变为了原来的1/n）
    - 通过主从同步读写分离扩展数据库性能：
      - 每个服务器上存储的数据量是和总量相同
      - n个服务器上的数据都一样，都是全集
      - 理论上读性能扩充了n倍，写仍然是单点，写性能不变
- 服务节点集群之前放一个集中式代理（proxy），由代理负责请求分发

  - 7层Nginx:response经过Proxy
  - 四层F5、LVS:response不经过proxy，如LVS
  - 在于方便控制，而且能容易实现一些更精密，更复杂的算法
  - 缺点
    - 负载均衡器本身可能成为性能瓶颈
    - 可能引入额外的延迟，请求一定先发到达负载均衡器，然后到达真正的服务节点。

  <!---->

  - load balancer proxy不能成为单点故障（single point of failure），因此一般会设计为高可用的主从结构
  - response也是走load balancer proxy的话，那么整个服务过程对客户端而言就是完全透明的，也防止了客户端去尝试连接后台服务器，提供了一层安全保障！

![grpc原理图](../_static/grpc.png "grpc原理图")
![proxy原理图](../_static/proxy.png "proxy原理图")

### 方案

- HTTP重定向：权衡转移请求开销和处理实际请求开销，前者相对于后者越小，那么重定向的意义就越大
  - web服务器可以通过http响应头信息中的Location标记来返回一个新的URL。这意味着HTTP代理需要继续请求这个新的URL，完成自动跳转。
  - 缺陷
    - 吞吐率限制：主站点服务器的吞吐率平均分配到了被转移的服务器现假设使用RR（Round Robin）调度策略，主服务器的吞吐与子服务器吞吐匹配
    - 重定向访问深度不同：实际服务器的负载差异是不可预料的，而主站服务器却一无所知
- 基于DNS负载均衡：可以实现在地域上流量均衡,DNS服务器充当负载均衡调度器
  - 使用域名系统通过将域名解析为服务器的不同 IP 地址来将请求分发到不同的服务器
  - 大型网站一般使用DNS作为第一级负载均衡,节省了所谓的主站点，DNS服务器充当主站点职能。常见策略是对多个A记录进行RR(轮询),dig命令查询
    - 在DNS服务器配置多个A记录，不同的DNS请求会解析到不同的IP地址 让DNS服务器根据不同地理位置的用户返回不同的IP
  - 相当于实现了按照「就近原则」将请求分流了，既减轻了单个集群的负载压力，也提升了用户的访问速度
  - 配置简单，实现成本非常低，无需额外的开发和维护工作
  - 缺点：
    - 大多是基于地域或者干脆直接做IP轮询，没有更高级的路由策略，所以这也是DNS方案的局限所在，比如 无法将HTTP请求的上下文引入到调度策略中
    - DNS生效时间略长，当配置修改后，生效不及时。这个是由于DNS的特性导致的，DNS一般会有多级缓存，所以当修改了DNS配置之后，由于缓存的原因，会导致IP变更不及时，从而影响负载均衡的效果
    - 容易导致服务器之间的动态负载不平衡，因此服务器很难处理其峰值负载。在 DNS 服务器上不能很好地选择名称映射的 TTL 值。
- 基于硬件负载均衡：用于大型服务器集群中的负载需求，F5 Network Big-IP
  - 完全通过硬件来抗压力，性能是非常的好。用在大型互联网公司的流量入口最前端
  - 优点：
    - 功能强大：支持各层级负载均衡及全面负载均衡算法
    - 性能强大：性能远超常见的软件负载均衡器
    - 稳定性高：硬件负载均衡，大规模使用肯定是严格测试过的
    - 安全防护：除具备负载均衡功能外，还具备防火墙、防 DDoS 攻击等安全功能
  - 缺点：
    - 价格昂贵
    - 可扩展性差
    - 调试维护麻烦
- 基于软件负载均衡：基于机器层面的流量均衡
  - 反向代理负载均衡｜七层负载均衡 :基于第七层应用层来做流量分发
    - 工作在HTTP层面，核心工作是转发HTTP
    - 任何对于实际服务器HTTP请求都必须经过调度器
    - 调度器必须等待实际服务器HTTP响应，并将它反馈给用户
    - 特性：
      - 调度策略丰富
      - 对反向代理服务器的并发处理能力要求高，因为它工作在HTTP层面
      - 反向代理服务器进行转发操作本身需要一定开销的，比如创建线程、与后端服务器建立TCP连接、接收后端服务器返回的处理结果、分析HTTP头部信息、用户空间和内核空间的频繁切换等，虽然这部分时间并不长，但是当后端服务器处理请求的时间非常短时，转发的开销就显得尤为突出。例如请求静态文件，更适合使用前面介绍的基于DNS的负载均衡方式
      - 反向代理服务器可以监控后端服务器，比如系统负载、响应时间、是否可用、TCP连接数、流量等，从而根据这些数据调整负载均衡的策略
      - 反射代理服务器可以让用户在一次会话周期内的所有请求始终转发到一台特定的后端服务器上（粘滞会话），这样的好处一是保持session的本地访问，二是防止后端服务器的动态内存缓存的资源浪费
    - Nginx：七层负载均衡 ，也称为“内容交换”，也就是主要通过报文中真正有意义的应用层内容
      - 传统：相对于传统基于进程或线程模型（Apache就采用这种模型）在处理并发连接时会为每一个连接建立一个单独的进程或线程，且在网络或者输入/输出操作时阻塞，将导致内存和 CPU 的大量消耗，因为新起一个单独的进程或线程需要准备新的运行时环境，包括堆和栈内存的分配，以及新的执行上下文，当然，这些也会导致多余的 CPU 开销。最终，会由于过多的上下文切换而导致服务器性能变差。
      - Nginx 的架构设计是采用模块化的、基于事件驱动、异步、单线程且非阻塞
  - [HAProxy](../../ops/HAProxy.md)
- 日 PV 小于1000万，用 Nginx 就完全可以了；如果机器不少，可以用 DNS 轮询，LVS 所耗费的机器还是比较多的；大型网站或重要的服务，且服务器比较多时，可以考虑用 LVS
- 合理流行架构方案：Web 前端采用 Nginx/HAProxy+Keepalived 作负载均衡器；后端采用 MySQL数据库一主多从和读写分离，采用 LVS+Keepalived 的架构
- Google于2016年3月最新公布的负载均衡Maglev
  - Maglev是谷歌为自己的数据中心研发的解决方案，并于2008开始用于生产环境。在第十三届网络系统设计与实现USENIX研讨会（NSDI '16）上， 来自谷歌、加州大学洛杉矶分校、SpaceX公司的工程师们分享了这一商用服务器负载均衡器Maglev的详细信息
  - Maglev安装后不需要预热5秒内就能应付每秒100万次请求令人惊叹不已。在谷歌的性能基准测试中，Maglev实例运行在一个8核CPU下，网络吞吐率上限为12M PPS(数据包每秒)，如果Maglev使用Linux内核网络堆栈则速度会小于4M PPS
- 国内云服务商 UCloud 进一步迭代了负载均衡产品----Vortex，成功地提升了单机性能
  - 在技术实现上，UCloud Vortex与Google Maglev颇为相似。以一台普通性价比的x86 1U服务器为例，Vortex可以实现吞吐量达14M PPS(10G, 64字节线速)，新建连接200k CPS以上，并发连接数达到3000万、10G线速的转发

## [keepalived](https://wsgzao.github.io/post/keepalived/)

- 运行在 lvs 之上，是一个用于做双机热备（HA）的软件，主要功能是实现真实机的故障隔离及负载均衡器间的失败切换，提高系统的可用性
  - keepalived 是 lvs 的扩展项目, 因此它们之间具备良好的兼容性
  - 对 RealServer 的健康检查, 实现对失效机器 / 服务的故障隔离
- 原理：keepalived 通过选举（看服务器设置的权重）挑选出一台热备服务器做 MASTER 机器，MASTER 机器会被分配到一个指定的虚拟 ip，外部程序可通过该 ip 访问这台服务器，如果这台服务器出现故障（断网，重启，或者本机器上的 keepalived crash 等），keepalived 会从其他的备份机器上重选（还是看服务器设置的权重）一台机器做 MASTER 并分配同样的虚拟 IP，充当前一台 MASTER 的角色
- 选举策略：根据 VRRP 协议，完全按照权重大小，权重最大（0～255）的是 MASTER 机器，下面几种情况会触发选举
  - keepalived 启动的时候
  - master 服务器出现故障（断网，重启，或者本机器上的 keepalived crash 等，而本机器上其他应用程序 crash 不算）
  - 有新的备份服务器加入且权重最大
- 配置
  - VRRPD 配置包括三个类:
    - VRRP 同步组(synchroization group)
    - VRRP 实例(VRRP Instance)
    - VRRP 脚本

```sh
# 全局定义 (global definition)
global_defs {
   notification_email {
   acassen@firewall.loc
   failover@firewall.loc
   sysadmin@firewall.loc
   }
   notification_email_from Alexandre.Cassen@firewall.loc
   smtp_server 192.168.200.1
   smtp_connect_timeout 30
   router_id LVS_DEVEL
}
#notification_email: 表示 keepalived 在发生诸如切换操作时需要发送 email 通知以及 email 发送给哪些邮件地址邮件地址可以多个每行一个
#notification_email_from admin@example.com: 表示发送通知邮件时邮件源地址是谁
#smtp_server 127.0.0.1: 表示发送 email 时使用的 smtp 服务器地址这里可以用本地的 sendmail 来实现
#smtp_connect_timeout 30: 连接 smtp 连接超时时间
#router_id node1: 机器标识，通常配置主机名

# 静态地址和路由配置范例
static_ipaddress {
    192.168.1.1/24 brd + dev eth0 scope global
    192.168.1.2/24 brd + dev eth1 scope global
}
static_routes {
    src $SRC_IP to $DST_IP dev $SRC_DEVICE
    src $SRC_IP to $DST_IP via $GW dev $SRC_DEVICE
}
# 这里实际上和系统里面命令配置 IP 地址和路由一样例如
# 192.168.1.1/24 brd + dev eth0 scope global 相当于: ip addr add 192.168.1.1/24 brd + dev eth0 scope global
# 就是给 eth0 配置 IP 地址路由同理, 一般这个区域不需要配置
# 这里实际上就是给服务器配置真实的 IP 地址和路由的在复杂的环境下可能需要配置一般不会用这个来配置我们可以直接用 vi /etc/sysconfig/network-script/ifcfg-eth1 来配置切记这里可不是 VIP 不要搞混淆了切记切记
```

### 算法

- 衡量标准
  - 是否意识到不同节点的服务能力是不一样的，比如CPU、内存、网络、地理位置
  - 是否意识到节点的服务能力是动态变化的，高配的机器也有可能由于一些突发原因导致处理速度变得很慢
  - 是否考虑将同一个客户端，或者说同样的请求分发到同一个处理节点，这对于“有状态”的服务非常重要，比如session，比如分布式存储
  - 谁来负责负载均衡，即谁充当负载均衡器（load balancer），balancer本身是否会成为瓶颈
- 方案
  - 轮询算法（round-robin）：提供同质服务的节点逐个对外提供服务，这样能做到绝对的均衡.
    - 没有考虑到节点的差异
  - 加权轮询算法（weight round-robin）:在轮训算法的基础上，考虑到机器的差异性，分配给机器不同的权重.依赖于请求的类型，比如计算密集型，那就考虑CPU、内存；如果是IO密集型，那就考虑磁盘性能
  - 随机算法（random）:随机选择一个节点服务，按照概率，只要请求数量足够多，那么也能达到绝对均衡的效果
  - 加权随机算法（random）:在随机的时候引入不同节点的权重
  - 哈希法（hash）：根据客户端的IP，或者请求的“Key”，计算出一个hash值，然后对节点数目取模。好处就是，同一个请求能够分配到同样的服务节点，这对于“有状态”的服务很有必要
    - 当节点的数目发生变化的时候，请求会大概率分配到其他的节点，引发到一系列问题
  - 一致性哈希算法：一个物理节点与多个虚拟节点映射，在hash的时候，使用虚拟节点数目而不是物理节点数目。当物理节点变化的时候，虚拟节点的数目无需变化，只涉及到虚拟节点的重新分配。而且，调整每个物理节点对应的虚拟节点数目，也就相当于每个物理节点有不同的权重
  - 最少连接算法（least connection）：根据节点的真实负载，动态地调整节点的权重就非常重要。当然，要获得接节点的真实负载也不是一概而论的事情，如何定义负载，负载的收集是否及时
    - 每个节点当前的连接数目是一个非常容易收集的指标，因此lease connection是最常被人提到的算法
  - 响应策略：将请求转发给当前时刻响应最快的后端服务器
    - 不停的去统计每一台后端服务器对请求的处理速度了

```python
SERVER_LIST = [
      '10.246.10.1',
     '10.246.10.2',
     '10.246.10.3',
 ]
 def round_robin(server_lst, cur = [0]):
     length = len(server_lst)
     ret = server_lst[cur[0] % length]
     cur[0] = (cur[0] + 1) % length
     return ret

 WEIGHT_SERVER_LIST = {
     '10.246.10.1': 1,
     '10.246.10.2': 3,
     '10.246.10.3': 2,
 }
 def weight_round_robin(servers, cur = [0]):
     weighted_list = []
     for k, v in servers.iteritems():
         weighted_list.extend([k] * v)

     length = len(weighted_list)
     ret = weighted_list[cur[0] % length]
     cur[0] = (cur[0] + 1) % length
     return ret

def random_choose(server_lst):
    import random
    random.seed()
    return random.choice(server_lst)

def weight_random_choose(servers):
    import random
    random.seed()
    weighted_list = []
    for k, v in servers.iteritems():
        weighted_list.extend([k] * v)
    return random.choice(weighted_list)

# 如果节点列表以及权重变化不大，那么也可以对所有节点归一化，然后按概率区间选择
def normalize_servers(servers):
    normalized_servers = {}
    total = sum(servers.values())
    cur_sum = 0
    for k, v in servers.iteritems():
        normalized_servers[k] = 1.0 * (cur_sum + v) / total
        cur_sum += v
    return normalized_servers

def weight_random_choose_ex(normalized_servers):
    import random, operator
    random.seed()
    rand = random.random()
    for k, v in sorted(normalized_servers.iteritems(), key = operator.itemgetter(1)):
        if v >= rand:
            return k
    else:
        assert False, 'Error normalized_servers with rand %s ' % rand

def hash_choose(request_info, server_lst):
     hashed_request_info = hash(request_info)
     return server_lst[hashed_request_info % len(server_lst)]
```

## [健壮系统](https://mp.weixin.qq.com/s/uYze9g54jd9DdmB92lX15w)

- 良好的软件系统架构设计
  - 系统架构：网络拓扑是什么、用什么存储、用什么缓存、整个数据流向是如何、那个核心服务采用那个开源软件支撑、用什么编程语言来构建整个软件连接各个服务、整个系统如何分层？
    - 架构师视角是不仅是完成整个项目，更多需要思考整个架构是否清晰、是否可维护、是否可扩展、可靠性稳定性如何，整个技术框架和各种体系选型是否方便容易开发维护；整个思考维度和视角是完全不一样的。程序员视角是执行层面具体编码的视角，架构师视角是设计师的视角，会更宏观，想的更远。
    - 服务架构链路要清晰,每一层各司其职:接入层（网关、负载均衡）、应用层（PHP程序等）、服务层（微服务接口等）、存储层（DB、缓存、检索ES等）、离线计算层（不一定包含，一般会以服务层或存储层出现）
    - 每个服务都需要考虑灾备或分布式，不能出现单点架构（持续进化）
    - 每个服务都必须考虑最优的技术选型（最佳实践）
    - 服务必须考虑熔断降级方案:把服务分层，切分一级核心服务、二级重要服务、三级可熔断服务等等区分，还需要有对应的预案
    - 运维部署回滚监控等系统需要快速高效
    - 编写的接口和前后端联合调试要方便快捷
      - 善于使用好的工具（比如Filder/Postman/SoapUI等），并且对应接口文档清晰，最好是能够通过一些工具生成好API文档（APIJson/Swagger/Eolinker）
    - 让整个系统完全可监控可追踪
      - 对应的trace系统（包含trace_id），把从接入层、应用层、服务层、存储层等都能够串联起来，每个环节出现的问题都可追踪，快速定位问题找到bug或者服务瓶颈短板；也能够了解整个系统运行情况和细节。（比如一些日志采集系统 OpenResty/Filebeat/Flume/LogStash/ELK）
    - 系统中的每个细节都是需要可以量化的，不能是模糊不明确的
      - 比如单个服务的QPS能力（预计流量需要多少服务器)、并发连接数（系统设置、系统承载连接）、单个进程内存占用、线程数、网络之间访问延迟时间（服务器之间延迟、机房到机房的延迟、客户端到服务器的延迟）、各种硬件性能参数（磁盘IO、服务器网卡吞吐量等）。
    - 让应用无状态化、容器化、微服务化
      - 去中心化、原子化、语言无依赖、独立自治、快速组合、自动部署、快速扩容，采用微服务+容器化来解决。
      - 阻碍横向扩展的最大的阻碍就是“有状态”，有状态就是有很多应用会存储私有的东西在应用运行的内存、磁盘中，而不是采用通用的分布式缓存、分布式存储解决方案，导致应用在容器化的情况下无法快速扩容，所以应用需要“去有状态化”，让应用全部“无状态化”。
      - 微服务化的逻辑是让的每个服务可以独立运行，比如说用户中心系统对外提供的不是代码级别的API，而是基于RESTfu或者gRPC协议的远程一个服务多个接口，这个服务或接口核心用来解决把整个用户中心服务变成独立服务，谁都可以调用，并且这个服务本身不会对内外部有太多的耦合和依赖，对外暴露的也只是一个个独立的远程接口而已。
      - 尽量把关键服务可以抽象成为一个个微服务，虽然微服务会增加网络调用的成本，但是每个服务之间的互相依赖性等等都降低了，并且通过容器技术，可以把单给微服务快速的横向扩展部署增加性能，虽然不是银弹，也是一个非常好的解决方案。
      - 基于容器的微服务化以后，整个业务系统从开发、测试、发布、线上运维、扩展 等多个方面都比较简单了，可以完全依赖于各种自动半自动化工具完成，整个人工干预参加的成分大幅减少。
  - 系统设计：采用什么编程语言、编程语言使用什么编程框架或中间件、使用什么设计模式来构建代码、中间代码如何分层？
  - 编程实现：编程语言用什么框架、有什么规范、编程语言需要注意哪些细节、有哪些技巧、那些编程原则？
- 编程最佳实践
  - 充分理解业务需求:保证理解业务后，整个程序设计符合需求或者未来几个月可以扩展，既不做过度设计，也不做各种临时硬编码。
  - 代码核心原则：KISS（Keep it simple,stupid）:来自于Unix编程艺术，你的东西必须足够简单足够愚蠢，好处非常多，比如容易读懂，容易维护交接，出问题容易追查等等。
  - 遵守编码规范，代码设计通用灵活:学会通过用函数和类进行封装（高内聚、低耦合）、如何定义函数，缩进方式，返回参数定义，注释如何定义、减少硬编码（通过配置、数据库存储变量来解决）
  - 设计模式和代码结构需要清晰:比如常规使用的MVC设计模式，为了就是把各个层次代码区分开。（M干好数据读取或者接口访问的事儿，C干好变量收发基本教研，V干好模板渲染或者api接口输出；M可以拆分成为：DAO数据访问层和Service某服务提供层）
  - 程序中一定要写日志，代码日志要记录清晰:（Info、Debug、Waring、Trace等等，调用统一的日志库，不要害怕多写日志）
  - 稳健性编程小技巧
    - 代码里尽量不要使用else
    - 所有的循环必须有结束条件或约定，并且不会不可控
    - 不要申请超级大的变量或内存造成资源浪费
    - 无论静态还是动态语言，内存或对象使用完以后尽量及时释放
    - 输入数据务必要校验，用户输入数据必须不可信。
    - 尽量不要使用异步回调的方式
  - 所有内外部访问都必须有超时机制：保证不连锁反应雪崩
    - 连接超时、读超时、写超时、通用超时
    - 一般超时粒度大部分都是秒为单位，对于时间敏感业务都是毫秒为单位，建议以毫秒(ms)为单位的超时更可靠，但是很多服务没有提供这类超时操作接口。
  - 成熟稳定的SQL语言使用习惯和技巧
    - 所有SQL语句都必须有约束条件
    - SQL查询里抽取字段中明确需要抽取的字段
    - 熟知各种SQL操作的最佳实践技巧，包括不限于：常用字段建立索引（单表不超过6个）、尽量减少OR、尽量减少连表查询、尽量不要SQL语句中使用函数（datetime之类）、使用exists代替in、使用explain观察SQL运行情况等等。
  - 开发中时刻要记得代码安全
    - SQL注入
    - XSS
    - CSRF
    - URL跳转漏洞
    - 文件上传下载漏洞
  - 调优后端服务的性能配置
- 健壮代码通用原则
  - 模块性原则：写简单的，通过干净的接口可被连接的部件。（比如类、函数，高内聚低耦合）
  - 清楚原则：清楚要比小聪明好。（代码中注释需要清晰明确，最好有历史迭代，不要耍小聪明，或者用一些奇怪的实现算法并且没注释）
  - 合并原则：设计能被其它程序连接的程序。（提供好输入输出参数，或者设计好的openapi，尽量让程序可以复用）
  - 简单原则：设计要简单；只有当你需要的时候，增加复杂性。（每个函数类要简单明确，不要太冗长）
  - 健壮性原则：健壮性是透明和简单的追随者。（透明+简单了，健壮就来了）
  - 沉默补救原则：当一个程序没有异常的时候就只是记录，减少干扰或者啥都不说；当你必须失败的时候，尽可能快的吵闹地失败。（失败了一定要明确清晰的提示形式，包括错误代码，错误原因的信息，不要悄无声息）
  - 经济原则：程序员的时间是宝贵的；优先机器时间节约它。（能够用内存+CPU搞定，不要过多纠结在算法上）
  - 产生原则：避免手工堆砌；当你可能的时候，编写可以写程序的程序。（用程序来帮你实现重复的事儿）
  - 优化原则：在雕琢之前先有原型；在你优化它之前，先让他可以运行。（先完成，再完美）
  - 可扩展原则：为将来做设计，因为它可能比你认为来的要快。（尽量考虑你这个代码2，3，5年后才会重构，为未来负责）
- 个人专业软素质
  - 细心：写完代码都需要重新Review一遍，变量名是否正确，变量是否初始化，每个SQL语句是否性能高超或者不会导致超时死锁；
  - 认真：每个函数是否都自己校验过输入输出是满足预期的；条件允许，是否核心函数都具备单元测试代码；
  - 谨慎：不要相信任何外部输入的数据，包括数据库、文件、缓存、用户HTTP提交各种变量，都需要严格校验和过滤。
  - 精进：不要惧怕别人说你代码烂，必须能够持续被人吐槽下优化，在在我革新下优化；要学习别人优秀的代码设计思想和代码风格，持续进步。
  - 专业：专业是一种工作态度，也是一种人生态度；代码要专业、架构要专业、变量名要专业、文档要专业、跟别人发工作消息邮件要专业、开会要专业、沟通要专业，等等，专业要伴随自己一生。

```sh
    # 核心性能影响配置

    # Linux系统
    ## 并发文件描述符 /etc/security/limits.conf
    *        soft    nofile  1000000
    *        hard    nofile  1000000
    ## Session临时修改
    ulimit -SHn 1000000

    # 进程数量限制 /etc/security/limits.d/20-nproc.conf
    *          soft    nproc  4096
    root     soft    nproc  unlimited

    # 文件句柄数量
    ## 临时修改
    echo 1000000 > /proc/sys/fs/file-max
    ## 永久修改
    echo "fs.file-max = 1000000" >>/etc/sysctl.conf
    ## 网络TCP选项，关注 *somaxconn/*backlog/*mem*系列/*time*系列等等
    ## 关闭SWAP交换分区（服务器卡死元凶）
    echo "vm.swappiness = 0">> /etc/sysctl.conf

    Nginx/OpenResty
    # Nginx Worker性能：
    worker_processes 4;
    worker_cpu_affinity 01 10 01 10;
    worker_rlimit_nofile 10240;
    worker_connections 10240;

    # Nginx网络性能：
    use epoll;
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 30;
    proxy_connect_timeout 10;

    # Nginx缓存配置：
    fastcgi_buffer_size 64k;
    client_max_body_size 300m;
    client_header_buffer_size 4k;
    open_file_cachemax=65535 inactive=60s;
    open_file_cache_valid 80s;
    proxy_buffer_size 256k;
    proxy_buffers 4256k;
    proxy_cache*

    # PHP/FPM
    listen.backlog = -1  #backlog数，-1表示无限制
    rlimit_files = 1024  #设置文件打开描述符的rlimit限制
    rlimit_core = unlimited #生成core dump文件限制，受限于linux系统
    pm.max_children = 256  #子进程最大数
    pm.max_requests = 1000 #设置每个子进程重生之前服务的请求数
    request_terminate_timeout = 0 #设置单个请求的超时中止时间
    request_slowlog_timeout = 10s  #当一个请求该设置的超时时间后

    # MySQL/MariaDB
    ## MySQL服务选项：
    wait_timeout=1800
    max_connections=3000
    max_user_connections=800
    thread_cache_size=64
    skip-name-resolve = 1
    open_tables=512
    max_allowed_packet = 64M

    ## MySQL性能选项：
    innodb_page_size = 8K #脏页大小
    innodb_buffer_pool_size = 10G #建议设置为内存80%
    innodb_log_buffer_size = 20M #日志缓存大小
    innodb_flush_log_at_trx_commit = 0  #事务日志提交方式，设置为0比较合适
    innodb_lock_wait_timeout = 30 #锁获取超时等待时间
    innodb_io_capacity = 2000 #刷脏页的频次默认200，高一些会让io曲线稳

    # Redis
    maxmemory  5000mb  #最大内存占用
    maxmemory-policy allkeys-lru  #达到内存占用后淘汰策略，存在热点数据，淘汰不咋访问的
    maxclients 1000 #客户端并发连接数
    timeout 150  #客户端超时时间
    tcp-keepalive 150  #向客户端发送tcp_ack探测存活
    rdbcompression no  #磁盘镜像压缩，开启占用cpu
    rdbchecksum no  #存储快照后crc64算法校验，增加10%cpu占用
    vm-enabled no #不做数据交换
```

## 资源

- [Hprose](https://hprose.com):高性能远程对象服务引擎
- [awesome-selfhosted](https://github.com/Kickball/awesome-selfhosted):This is a list of Free Software network services and web applications which can be hosted locally. Selfhosting is the process of locally hosting and managing applications instead of renting from SaaS providers. <https://reddit.com/r/selfhosted>
- [Back-End-Developer-Interview-Questions](https://github.com/arialdomartini/Back-End-Developer-Interview-Questions):A list of back-end related questions you can be inspired from to interview potential candidates, test yourself or completely ignore
- [Backend-Series](https://github.com/wx-chevalier/Backend-Series):📚 服务端应用程序开发与系统架构/微服务架构与实践，服务端基础篇 | 微服务与云原生篇 | Spring 篇 | Node.js 篇 | DevOps 篇 | 信息安全与渗透测试篇
- [TechClass](https://github.com/lemonchann/TechClass):项目涵盖成为一个后端开发程序员必备的技能，包括Linux、网络、架构、微服务、数据库、数据结构和算法、编程语言学习等内容 <https://lemonchann.github.io/TechClass>

## 参考

- [camel](https://github.com/dianping/camel):软负载一体解决方案，承担了F5硬负载层后的软负载工作
- [cilium](https://github.com/cilium/cilium):API Aware Networking and Security using BPF and XDP
