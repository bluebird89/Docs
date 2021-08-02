## [Calico](https://github.com/projectcalico/calico)

Cloud native networking and network security

[docs.projectcalico.org](http://docs.projectcalico.org "http://docs.projectcalico.org")

## 原理

- 不走 Overlay 网络，不引入另外的网络性能损耗，而是将转发全部用三层网络的路由转发来实现
- 如果全部走三层的路由规则，没必要每台机器都用一个 docker0，从而浪费了一个 IP 地址，而是可以直接用路由转发到 veth pair 在物理机这一端的网卡。同样，在容器内，路由规则也可以这样设定：把容器外面的 veth pair 网卡算作默认网关，下一跳就是外面的物理机。
- 物理机化身为路由器，通过路由器上的路由规则，将包转发到目的地。在这个过程中，没有隧道封装解封装，仅仅是单纯的路由转发，性能会好很多
- 容器 A1 的 IP 地址为 172.17.8.2/32，将容器 A1 作为一个单点的局域网
	- 容器 A1 里面的默认路由 169.254.1.1,没有一张网卡是这个地址
		- 当一台机器要访问网关的时候，首先会通过 ARP 获得网关的 MAC 地址，然后将目标 MAC 变为网关的 MAC，而网关的 IP 地址不会在任何网络包头里面出现，也就是说，没有人在乎这个地址具体是什么，只要能找到对应的 MAC，响应 ARP 就可以了。
	- 网关 MAC 地址是 Calico 硬塞进去的，能响应 ARP，于是发出的包的目标 MAC 就是这个 MAC 地址。
- 物理机 A 上查看所有网卡的 MAC 地址的时候，发现 veth1 就是这个 MAC 地址。所以容器 A1 里发出的网络包，第一跳就是这个 veth1 这个网卡，也就到达了物理机 A 这个路由器。
- 在物理机 A 上有三条路由规则，分别是去两个本机的容器的路由，以及去 172.17.9.0/24，下一跳为物理机 B。

![[calico_struct.png]]

```sh
default via 169.254.1.1 dev eth0 
169.254.1.1 dev eth0 scope link

ip neigh
# 169.254.1.1 dev eth0 lladdr ee:ee:ee:ee:ee:ee STALE

172.17.9.2 dev veth1 scope link 
172.17.9.3 dev veth2 scope link 
172.17.8.0/24 via 192.168.100.100 dev eth0 proto bird onlink
```

## 架构

- 路由配置组件 Felix
	- 如果只有两台机器，每台机器只有两个容器，而且保持不变。手动配置一下，倒也没啥问题。但是如果容器不断地创建、删除，节点不断地加入、退出，情况就会变得非常复杂。
	- 有三台物理机，两两之间都需要配置路由，每台物理机上对外的路由就有两条。如果有六台物理机，则每台物理机上对外的路由就有五条。新加入一个节点，需要通知每一台物理机添加一条路由。这还是在物理机之间，一台物理机上，每创建一个容器，也需要多配置一条指向这个容器的路由。
	- 如此复杂，肯定不能手动配置，需要每台物理机上有一个 agent，当创建和删除容器的时候，自动做这件事情。这个 agent 在 Calico 中称为 Felix。
- 路由广播组件 BGP Speaker
	- 如何将路由信息，即将“如何到达我这个节点，访问我这个节点上的容器”这些信息，广播出去
	- 所有 Node 上的 BGP Speaker 都互相建立连接，就形成了全互连的情况，这样每当路由有所变化的时候，所有节点就都能够收到了。
- 安全策略组件 Network Policy
	- 灵活配置两个容器通或者不通
	- 虚拟机中的安全组用 iptables 实现的, 在内核处理网络包的过程中可以嵌入的处理点。Calico 也是在这些点上设置相应的规则。
	- 当网络包进入物理机上的时候，进入 PREOUTING 规则，规则 cali-fip-dnat，实现浮动 IP（Floating IP）的场景，主要将外网的 IP 地址 dnat 作为容器内的 IP 地址。在虚拟机场景下，路由器的网络 namespace 里面有一个外网网卡上，也设置过这样一个 DNAT 规则。
	- 接下来根据路由判断，是到本地的，还是要转发出去的。如果是本地的，走 INPUT 规则，里面有规则 cali-wl-to-host，wl 的意思是 workload，也即容器，也即这是用来判断从容器发到物理机的网络包是否符合规则的。
	- 里面内嵌一个规则 cali-from-wl-dispatch，也是匹配从容器来的包。
	- 如果有两个容器，则会有两个容器网卡，这里面内嵌有详细的规则“cali-fw-cali 网卡 1”和“cali-fw-cali 网卡 2”，fw 就是 from workload，也就是匹配从容器 1 来的网络包和从容器 2 来的网络包。
	- 如果是转发出去的，走 FORWARD 规则，里面有个规则 cali-FORWARD。两种情况，
		- 一种是从容器里面发出来，转发到外面的,则仍然是 cali-from-wl-dispatch，也即 from workload
		- 另一种是从外面发进来，转发到容器里面的,匹配规则是 cali-to-wl-dispatch，也即 to workload。
	- 如果有两个容器，则会有两个容器网卡，在这里面内嵌有详细的规则“cali-tw-cali 网卡 1”和“cali-tw-cali 网卡 2”，tw 就是 to workload，也就是匹配发往容器 1 的网络包和发送到容器 2 的网络包。
	- 接下来匹配 OUTPUT 规则，里面有 cali-OUTPUT。
	- 接下来是 POSTROUTING 规则，里面有一个规则是 cali-fip-snat，也即发出去的时候，将容器网络 IP 转换为浮动 IP 地址。在虚拟机场景下，路由器的网络 namespace 里面有一个外网网卡上，也设置过这样一个 SNAT 规则。
- BGP Route Reflector
	- 用 [BIRD](https://bird.network.cz/?get_doc&f=bird.html&v=20) 实现
	- 有了它，BGP Speaker 就不用全互连了，而是都直连它，负责将全网的路由信息广播出去。
	- 应该有多个 BGP Router Reflector，每个 BGP Router Reflector 管一部分
	- 一个机架上有多台机器，每台机器上面启动多个容器，每台机器上都有可以到达这些容器的路由。每台机器上都启动一个 BGP Speaker，然后将这些路由规则上报到这个 Rack 上接入交换机的 BGP Route Reflector，将这些路由通过 iBGP 协议告知到接入交换机的三层路由功能。
	- 在接入交换机之间也建立 BGP 连接，相互告知路由，因而一个 Rack 里面的路由可以告知另一个 Rack。有多个核心或者汇聚交换机将接入交换机连接起来，如果核心和汇聚起二层互通的作用，则接入和接入之间之间交换路由即可。如果核心和汇聚交换机起三层路由的作用，则路由需要通过核心或者汇聚交换机进行告知。
- 跨网段(物理机)访问
	- IPIP 模式 在物理机 A 和物理机 B 之间打一个隧道，这个隧道有两个端点，在端点上进行封装，将容器的 IP 作为乘客协议放在隧道里面，而物理主机的 IP 放在外面作为承载协议。这样不管外层的 IP 通过传统的物理网络，走多少跳到达目标物理机，从隧道两端看起来，物理机 A 的下一跳就是物理机 B

![[calico_policy.png]]
![[calico_arch.png]]

```sh
172.17.8.2 dev veth1 scope link 
172.17.8.3 dev veth2 scope link 
172.17.9.0/24 via 192.168.200.101 dev tun0 proto bird onlink
```

## 图书

* BGP in the datacenter

## 参考

* [使用 Prometheus-Operator 监控 Calico](https://mp.weixin.qq.com/s/QJp69EeZgIO3WUPfzCRv-w)
