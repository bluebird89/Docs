## firewall

#linux #security

- 一种网络隔离工具，部署于主机或者网络的边缘，目标是对于进出主机或者本地网络的网络报文根据事先定义好的规则做匹配检测，规则匹配成功则对相应的网络报文做定义好的处理（允许，拒绝，转发，丢弃等）
- 根据管理范围来分可以将其划分为主机防火墙和网络防火墙
- 根据工作机制来区分又可分为包过滤型防火墙（netfilter）和代理服务器（Proxy）

## [The Netfilter/Iptables Project](http://www.netfilter.org)

- 包过滤型防火墙 依赖于 Linux 内核软件 netfilter，一个 Linux 内核“安全框架”
- The netfilter is a set of hooks inside the Linux kernel that allows kernel modules to register callback functions with the network stack. A registered callback function is then called back for every packet that traverses the respective hook within the network stack.
  - 当主机/网络服务器网卡收到一个数据包之后进入内核空间网络协议栈进行层层解封装
  - 进入网络层数据包通过 PRE_ROUTING 关卡时，要进行一次路由选择，当目标地址为本机地址时，数据进入 INPUT，非本地的目标地址进入 FORWARD（需要本机内核支持 IP_FORWARD），目标地址转换通常在这个关卡进行
    - PreRouting -> Input -> Process -> Output -> PostRouting
    - PreRouting -> Forward -> PostRouting
  - INPUT 过滤 INPUT 包在此点关卡进行
  - FORWARD 网络防火墙通常在此关卡配置
  - OUTPUT 由本地用户空间应用进程产生数据包过此关卡， OUTPUT 包过滤在此关卡进行
  - POST_ROUTING 通过 FORWARD 和 OUTPUT 关卡的数据包要通过一次路由选择由哪个接口送往网络中，源地址转换通常在此点进行
- the packet filtering technology that’s built into the 2.4 Linux kernel.just the command used to control netfilter, which is the real underlying technology

![How Traffic Moves Through Netfilter](../_static/netfilter.jpg "Optional title")
![Packet flow in Netfilter and General Networking](../_static/Netfilter-packet-flow.svg "Optional title")

```sh
IF network_pkg match rule; THEN
    handler
FI
```

## ip_tables

- iptables 是内核软件 netfilter 的配置工具，工作于用户空间。
- iptables/netfilter 组合是 Linux 平台下过滤型防火墙，并且免费，用来替代商业防火墙软件，来完成网络数据包的过滤、修改、重定向以及网络地址转换（nat）等功能
- The iptables firewall works by interacting with the packet filtering hooks in the Linux kernel’s networking stack. These kernel hooks are known as the netfilter framework
- This Linux based firewall is controlled by the program called iptables to handles filtering for IPv4, and ip6tables handles filtering for IPv6.
- [iptables-essentials](https://github.com/trimstray/iptables-essentials):Iptables Essentials: Common Firewall Rules and Commands.
- 在五个节点上埋下函数，从而可以根据规则进行包的处理。按功能可分为四大类
  - 连接跟踪（conntrack） 基础功能,被其他功能所依赖
  - 数据包的过滤（filter）实现包的过滤、修改和网络地址转换
  - 网络地址转换（nat）实现包的过滤、修改和网络地址转换
  - 数据包的修改（mangle）实现包的过滤、修改和网络地址转换
- 在用户态，客户端程序 iptables，用命令行来干预内核的规则
- 使用 iptables 配置规则时，往往是以“表”为入口制定“规则
- 数据包经过一个关卡的时候，会将“链”中所有的“规则”都按照顺序逐条匹配
- 横向是chains,纵向是tables

![[ip_tables_arch.png]]

### config

- `/etc/sysconfig/iptables`
- `etc/sysconfig/iptables-config`
  - `IPTABLES_MODULES="ip_conntrack_ftp"`

```sh
*filter
# Drop All Traffic
# :INPUT ACCEPT [0:0]
# :FORWARD ACCEPT [0:0]
# :OUTPUT ACCEPT [0:0]
:INPUT DROP [0:0]
:FORWARD DROP [0:0]

:RH-Firewall-1-INPUT - [0:0]
-A INPUT -j RH-Firewall-1-INPUT
-A FORWARD -j RH-Firewall-1-INPUT
-A RH-Firewall-1-INPUT -i lo -j ACCEPT
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
-A RH-Firewall-1-INPUT -p udp --dport 5353 -d 224.0.0.251 -j ACCEPT
-A RH-Firewall-1-INPUT -p udp -m udp --dport 53 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 53 -j ACCEPT

# Log And Drop All Traffic
# -A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited
-A RH-Firewall-1-INPUT -j LOG
-A RH-Firewall-1-INPUT -j DROP

# Log and Drop Spoofing Source Addresses
-A INPUT -i eth0 -s 10.0.0.0/8 -j LOG --log-prefix "IP DROP SPOOF "
-A INPUT -i eth0 -s 172.16.0.0/12 -j LOG --log-prefix "IP DROP SPOOF "
-A INPUT -i eth0 -s 192.168.0.0/16 -j LOG --log-prefix "IP DROP SPOOF "
-A INPUT -i eth0 -s 224.0.0.0/4 -j LOG --log-prefix "IP DROP MULTICAST "
-A INPUT -i eth0 -s 240.0.0.0/5 -j LOG --log-prefix "IP DROP SPOOF "
-A INPUT -i eth0 -d 127.0.0.0/8 -j LOG --log-prefix "IP DROP LOOPBACK "
-A INPUT -i eth0 -s 169.254.0.0/16  -j LOG --log-prefix "IP DROP MULTICAST "
-A INPUT -i eth0 -s 0.0.0.0/8  -j LOG --log-prefix "IP DROP "
-A INPUT -i eth0 -s  240.0.0.0/4  -j LOG --log-prefix "IP DROP "
-A INPUT -i eth0 -s  255.255.255.255/32  -j LOG --log-prefix "IP DROP  "
-A INPUT -i eth0 -s 168.254.0.0/16  -j LOG --log-prefix "IP DROP "
-A INPUT -i eth0 -s 248.0.0.0/5  -j LOG --log-prefix "IP DROP "

# Open Port
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 80 -j ACCEPT
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 443 -j ACCEPT
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 53 -j ACCEPT
-A RH-Firewall-1-INPUT -m udp -p tcp --dport 53 -j ACCEPT
-A RH-Firewall-1-INPUT -m tcp -p tcp --dport 25 -j ACCEPT

# Only allow SSH traffic From 192.168.1.0/24
-A RH-Firewall-1-INPUT -s 192.168.1.0/24 -m state --state NEW -p tcp --dport 22 -j ACCEPT

COMMIT
```

### Packet Matching Rules

- Each packet starts at the first rule in the chain
  - 根据协议报文特征指定匹配条件，基本匹配条件和扩展匹配条件
- A packet proceeds until it matches a rule
- If a match found, then control will jump to the specified target (such as REJECT, ACCEPT, DROP)

### CHAINS

- lists of rules within a table, and they are associated with “hook points” on the system
- 当报文经过某一个关卡时，关卡上的“规则”不止一条，很多条规则会按照顺序逐条匹配，将在此关卡的所有规则组织称“链”就很适合，对于经过相应关卡的网络数据包按照顺序逐条匹配“规则”。
- PREROUTING（路有前规则）: Immediately after being received by an interface.
- INPUT(入站规则): Right before being handed to a local process
  - The default chain is used for packets addressed to the system.
  - Use this to open or close incoming ports (such as 80,25, and 110 etc) and ip addresses / subnet (such as 202.54.1.20/29).
- FORWARD（转发规则）: For any packets coming in one interface and leaving out another.
  - The default chains is used when packets send through another interface.
  - Usually used when you setup Linux as router.
  - For example, eth0 connected to ADSL/Cable modem and eth1 is connected to local LAN. Use FORWARD chain to send and receive traffic from LAN to the Internet.
- OUTPUT（出站规则）: Right after being created by a local process.
  - The default chain is used when packets are generating from the system.
  - Use this open or close outgoing ports and ip addresses / subnets.
- POSTROUTING（路由后规则）: Right before leaving an interface.
- RH-Firewall-1-INPUT a user-defined custom chain. It is used by the INPUT, OUTPUT and FORWARD chains.
  - 使用 iptables 创建自定义的链，附加到 iptables 的内置的五个链
- Packet
  - Stateful Packet Inspection SPI
  - Packets move through netfilter by traversing chains
  - By default, chain policies are to jump to the ACCEPT target

### TABLES

- 分为四种 raw-->mangle-->nat-->filter。优先级依次降低，raw 不常用，所以主要功能都在其他三种表里实现。每个表可以设置多个链
- raw
  - 关闭 nat 表上启用的连接追踪机制
  - 与之对应的内核模块 iptables_raw
  - PreRouting, Output
- MANGLE
  - used to otherwise modify packets, i.e. modifying various portions of a TCP header, etc.解包报文、修改并封包
  - 与之对应的内核模块 iptables_mangle
  - Prerouting
  - Postrouting
  - Input
  - Output
  - Forward
- NAT(Network Address Translation)
  - used to rewrite the source and/or destination of packets and/or track connections.
  - 网络地址转换功能，典型的比如 Snat（改变数据包的源地址）、Dnat（改变数据包的目标地址）
  - 与之对应的内核模块 iptables_nat
  - Prerouting 在数据包到达防火墙时改变目标地址
  - Postrouting 在数据包离开防火墙时改变数据包的源地址
  - Output 改变本地产生的数据包的目标地址
- FILTER
  - used for the standard processing of packets, and it’s the default table if none other is specified.负责过滤功能；
  - 与之对应的内核模块 iptables_filter
  - Input 过滤所有目标地址是本机的数据包
  - Output 过滤所有由本机产生的数据包
  - Forward 滤所有路过本机的数据包

![数据包经过过滤型防火墙的流程](../_static/packet_flow.png "Optional title")

### TARGETS

- determine what will happen to a packet within a chain if a match is found with one of its rules
- ACCEPT： allow packet.
- REJECT： to drop the packet and send an error message to remote host.
- DROP： drop the packet and do not send an error message to remote host or sending host
- QUEUE  发送给某个用户态进程处理
  - 实现负载均衡
    - k8s的kube-proxy 利用 iptables 做流量转发和负载均衡的，service 利用 nat 将相应流量转发到对应的pod中，另外iptables 有一个probability特性，可以设置probability的百分比是多少，从而实现负载均衡

```sh
firewall-cmd --get-active-zones # List active firewall zones
-–change-interface eth0 --zone=example # Place eth0 into example zone
--get-services # List all defined services
--add-service samba --zone=example # Add samba ports to example zone
--add-port=123/tcp --zone=example # Add port 123 to example zone
--permanent # Add this flag to make a change persistent
```

### 规则

- 流程
  - 数据包进入，先进 mangle 表 PREROUTING 链，根据需要，改变数据包头内容之后
  - 进入 nat 表的 PREROUTING 链，根据需要做 Dnat 目标地址转换
  - 路由判断，是进入本地还是转发
  - 进入本地的，进入 INPUT 链，按条件过滤限制进入
  - 如果是转发就进入 FORWARD 链，根据条件过滤限制转发
  - 进入 OUTPUT 链，按条件过滤限制出去，离开本地
  - 进入 POSTROUTING 链，可以做 Snat
  - 离开网络接口
- 考量
  - 根据要实现哪种功能，判断添加在哪张“表”上
  - 根据报文流经路径，判断添加在哪个“链”上
- 对于每一条“链”上其“规则”的匹配顺序，排列好检查顺序能有效的提高性能，因此隐含一定法则：
  - 同类规则（访问同一应用），匹配范围小的放上面
  - 不同类规则（访问不同应用），匹配到报文频率大的放上面
  - 将那些可由一条规则描述的多个规则合并为一个
  - 设置默认策略
- 在远程连接主机配置防火墙时注意：
  - 不要把“链”的默认策略修改为拒绝，因为有可能配置失败或者清除所有策略后无法登陆到服务器，而是尽量使用规则条目配置默认策略
  - 为防止配置失误策略把自己也拒掉，可在配置策略时设置计划任务定时清除策略，当确定无误后，关闭该计划任务

![数据包链路表](../_static/packet_link_map.jpg)

### 语法

- `iptables -t 表名 <-A/I/D/R> 规则链名 [规则号] <-i/o 网卡名> -p 协议名 <-s 源IP/源子网> --sport 源端口 <-d 目标IP/目标子网> --dport 目标端口 -j 动作`
  - -h 显示帮助信息
  - `!` 表示取反

- ` -L|--list [chain [rulenum]]  ` 列出[链 chain 上]所有规则  List the rules in a chain or all chains
  - --line-numbers
  - --list-rules -S [chain [rulenum]] Print the rules in a chain or all chins
  - -n Display IP address and port in numeric format. Do not use DNS to resolve names. This will speed up listing.
  - -v Display detailed information. This option makes the list command show the interface name, the rule options, and the TOS masks. The packet and byte counters are also listed, with the suffix ‘K’, ‘M’ or ‘G’ for 1000, 1,000,000 and 1,000,000,000 multipliers respectively.

- `-p protocol tcp|udp|icmp` 指定匹配数据包协议类型

- `-i|--in-interface [!] <网络接口name>` 指定数据包的来自网络接口，比如最常见的 eth0
  - 只对 INPUT，FORWARD，PREROUTING 这三个链起作用。
  - 如果没有指定此选项， 说明可以来自任何一个网络接口

- `-o|--out-interface [!] <网络接口name>` 指定数据包出去网络接口
  - 只对 OUTPUT，FORWARD，POSTROUTING 三个链起作用

- `-s|--source [!] address[/mask]` 把指定的一个／一组地址作为源地址，按此规则进行过滤
  - 没有 mask 时，是一个地址，比如：192.168.1.1
  - 当 mask 指定时，表示一组范围内地址，比如：192.168.1.0/255.255.255.0

- `-d|--destination [!] address[/mask]` 格式同上,指定地址为目的地址

- –dport num  匹配目标端口号

- –sport num  匹配来源端口号

- `-C|--check  chain` Check for the existence of a rule

- `-P|--policy chain target` 为指定链 chain 设置策略 target
  - 设置默认策略,Set the default policy (such as DROP, REJECT, or ACCEPT). `iptables -P INPUT DROP`
  - 只有内置的链才允许有策略，用户自定义的是不允许的

- `-A|--append chain rule-specification` 在指定链 chain 末尾插入指定规则

- `-I|--insert chain [rulenum=1] rule-specification` 在链 chain 中指定位置插入一条或多条规则  Insert in chain as rulenum (default 1=first)

- `-D|--delete chain rulenum` 在指定链 chain 中删除一个或多个指定规则 Delete rule rulenum (1 = first) from chain

- `-R|--replace  chain rulenum` Replace rule rulenum (1 = first) in chain

- -S specific chain (INPUT, OUTPUT, TCP, etc.)

- -N|--new chain 用指定的名字创建一个新的链  Create a new user-defined chain

- `-F|--flush [chain]` 清空指定链 chain 上所有规则。如果没有指定链，清空该表上所有链的所有规则 Deleting (flushing) all the rules.

- -`X|--delete-chain [chain]`   Delete a user-defined chain 删除指定链，这个链必须没有被其它任何规则引用，而且这条上必须没有任何规则。如果没有指定链名，则会删除该表中所有非内置的链

- -t table_name  Select table (called nat or mangle) and delete/flush rules

- `-Z|--zero [chain [rulenum]]` Zero counters in chain or all chains,Resetting Packet Counts and Aggregate Size

- `-j|--jump target <指定目标>` 满足某条件时该执行什么样的动作。target 可以是内置的目标，比如 ACCEPT，也可以是用户自定义的链

- `-E|--rename-chain  old-chain new-chain` Change chain name, (moving any reerences)

- state:makes netfilter a “stateful” firewalling technology. Packets are not able to move through this rule and get back to the client unless they were created via the rule above it

- –icmp-type

- echo request

```sh
chkconfig iptables on|off # forever
chkconfig iptables start|stop # recover with restart
service iptables stop|start|restart

# Save Firewall Rules
/etc/init.d/iptables status|save

# list out all of the active iptables rules
iptables -L [INPUT|OUTPUT] -n -v --line-numbers

# 设置默认 chain 策略
iptables -P INPUT DROP 
iptables -P FORWORD DROP
iptables -P OUTPUT DROP

iptables -A INPUT -p tcp --drop 端口号 -j DROP|ACCEPT
iptables -A OUTPUT -p tcp --dport 端口号 -j DROP # 关闭端口
iptables -I 5 INPUT -p tcp --dport 80 -j ACCEPT # open port

# 用户自定义链
iptables -t nat -N CLASH
iptables -t nat -A CLASH -d 10.0.0.0/8 -j RETURN
iptables -t nat -A CLASH -d 127.0.0.0/8 -j RETURN
iptables -t nat -A CLASH -d 169.254.0.0/16 -j RETURN
iptables -t nat -A CLASH -d 172.16.0.0/12 -j RETURN
iptables -t nat -A CLASH -d 192.168.0.0/16 -j RETURN
iptables -t nat -A CLASH -d 224.0.0.0/4 -j RETURN
iptables -t nat -A CLASH -d 240.0.0.0/4 -j RETURN
iptables -t nat -A CLASH -p tcp -j REDIRECT --to-ports 7892

# Allow Outgoing (Stateful) Web Browsing
# adding (appending) a rule to the OUTPUT chain for protocol TCP and destination port 80 to be allowed
iptables -A OUTPUT -o eth0 -p TCP –dport 80 -j ACCEPT
# allows the web traffic to come back
iptables -A INPUT -i eth0 -p TCP -m state –state ESTABLISHED,RELATED –sport 80 -j ACCEPT

# Allowing Outgoing Pings
iptables -A OUTPUT -o eth0 -p icmp –icmp-type echo-request -j ACCEPT
iptables -A INPUT -i eth0 -p icmp –icmp-type echo-reply -j ACCEPT

# “Passing Ports” Into A NATd Network  pass traffic inside to hidden servers
# DNAT occurs
iptables -t nat -A PREROUTING -i eth0 -p tcp -d 1.2.3.4 –dport 25 -j DNAT –to 192.168.0.2:25
# rules portion：make it through your firewall;
iptables -A FORWARD -i eth0 -o eth1 -p tcp –dport 25 -d 192.168.0.2 -j ACCEPT

iptables-save > /etc/iptables.up.rules
/sbin/iptables-restore < /etc/iptables.up.rules

# 删除
iptables -F  
iptables -X  
iptables -t nat -F  
iptables -t nat -X  
iptables -t mangle -F  
iptables -t mangle -X  
```

### For DoS and Syn Protection

```sh
## /etc/sysctl.conf
net.ipv4.conf.all.log_martians = 1
net.ipv4.conf.default.accept_source_route = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.default.secure_redirects = 0
net.ipv4.icmp_echo_ignore_broadcasts = 1
#net.ipv4.icmp_ignore_bogus_error_messages = 1
net.ipv4.tcp_syncookies = 1
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1
```

## UFW uncomplicated firewall

- default polices are defined in the /etc/default/ufw file
- can be changed either by manually modifying the file or with the `sudo ufw default <policy> <chain>` command
- config:`/etc/default/ufw`
  - Enabling IPv6 `IPV6=yes`
  - log:`/var/log/ufw.log`
  - /etc/ufw/before.rules
- rule
  - allow|deny
    - in on
  - limit normally allow the connection but will deny connections if an IP address attempts to initiate six or more connections within thirty seconds
  - proto
  - from
    - ip
    - 103.13.42.13/29
  - to
    - ip
    - any
  - port
    - tcp

```sh
# 防火墙
sudo apt install ufw
sudo ufw status
sudo ufw status verbose

sudo ufw enable/disable|reset
sudo ufw app list
sudo ufw app info 'Nginx Full'

# ufw allow port_number/protocol
sudo ufw allow 'Nginx HTTP'
sudo ufw allow https|ssh
sudo ufw allow 443
sudo ufw allow 7722/tcp
sudo ufw allow proto tcp to any port 80
sudo ufw allow 7100:7200/udp

sudo ufw allow from 64.63.62.61
sudo ufw allow from 64.63.62.61 to any port 22
sudo ufw allow from 192.168.1.0/24 to any port 3306
sudo ufw allow in on eth2 to any port 3306

sudo ufw deny from 23.24.25.0/24
sudo ufw deny proto tcp from 23.24.25.0/24 to any port 80,443

sudo ufw status numbered
sudo ufw delete 3
sudo ufw delete allow 8069

# /etc/ufw/sysctl.conf
net/ipv4/ip_forward=1
DEFAULT_FORWARD_POLICY="ACCEPT"

# /etc/ufw/before.rules
#NAT table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Forward traffic through eth0 - Change to public network interface
-A POSTROUTING -s 10.8.0.0/16 -o eth0 -j MASQUERADE

# don't delete the 'COMMIT' line or these rules won't be processed
COMMIT

bash <(curl -s https://git.jacksgong.com/Jacksgong/script/raw/master/firewall.sh)

# 查看某一端口的占用情况
[sudo ]lsof -i : (port)
# 显示tcp，udp的端口和进程等相关
netstat -tunlp
# 指定端口号进程情况
netstat -tunlp|grep (port)
# 进程查看
ps -ef | grep nginx
ps aux | grep nginx
lsof -Pni4 | grep LISTEN | grep php
# 关闭进程
kill -9 pid

No route to host iptables
```

```sh
sudo apt-get install ufw

sudo systemctl status ufw.service
sudo ufw status [verbose]

sudo ufw enable|disable

# edit UFW' configuration file /etc/ufw/before.rules,eed to run reload
sudo ufw reload

# default policy
sudo ufw default allow outgoing
sudo ufw default deny incoming

# allow
sudo ufw allow ssh
sudo ufw allow 2375/tcp
sudo ufw allow proto tcp from 202.54.2.5 to 172.24.13.45 port 22
sudo ufw limit ssh

sudo ufw allow 25
sudo ufw allow 3000:5000/tcp
sudo ufw allow from 1.2.3.4
sudo ufw allow proto tcp from any to 10.8.0.1 port 22
sudo ufw allow proto tcp from 10.8.0.2 to 10.8.0.1 port 22
sudo ufw allow from 1.2.3.4 to any port 22 proto tcp
sudo ufw allow from 1.2.3.4 to 222.222.222.222 port 22 proto tcp

# incoming HTTP traffic (open port 80)
sudo ufw allow http comment 'Allow all to access Apache server'
sudo ufw allow 80/tcp comment 'accept Apache'
## allow only from 139.1.1.1 ##
sudo ufw allow from 139.1.1.1 to any port 80
## allow only from 203.11.11.2/29 ##
sudo ufw allow from 203.11.11.2/29 to any port 80

# allow incoming HTTPS traffic 允许访问
sudo ufw allow 443/tcp comment 'accept HTTPS connections'
sudo ufw allow https comment 'Allow all to access Nginx server'
sudo ufw allow from 139.1.1.1 to any port 443
sudo ufw allow from 203.11.11.2/29 to any port 443

sudo ufw allow from 192.168.1.0/24 to any port 3306
# Allow access to MySQL/MariaDB port 3306 Apache server only:
sudo ufw allow from 202.54.1.1 to any port 3306

# interface
sudo ufw allow in on wg0 to any port 22
sudo ufw allow in on lxdbr0 from 10.105.28.22 to any port 3306 proto tcp
# add sub/net
sudo ufw allow in on lxdbr0 from 10.105.28.0/24 to any port 3306 proto tcp

## block
sudo ufw deny from 203.5.1.43
sudo ufw deny from 103.13.42.13/29
sudo ufw deny from 1.1.1.2 to any port 22 proto tcp

## comment
ufw allow 53 comment 'open tcp and udp port 53 for dns'
sudo ufw allow proto tcp from any to any port 80,443 comment 'my cool web app ports'sudo ufw allow proto tcp from any to 10.8.0.1 port 22 'SSHD port 22 for private lan'

# delete
sudo ufw status numbered
sudo ufw delete 6
sudo ufw delete allow 443

# reset
sudo ufw reset

# log
grep 'DPT=22' /var/log/ufw.log |\
egrep -o 'SRC=([0-9]{1,3}[\.]){3}[0-9]{1,3}' |\
awk -F'=' '{ print $2 }' | sort -u

# Show the list of rules
sudo ufw show listening

# report
sudo ufw show raw
sudo ufw show added
```

```sh
    # /etc/ufw/before.rules
    -A ufw-before-input -i eth0 -j ACCEPT
    -A ufw-before-output -o eth0 -j ACCEPT
```

### Masquerading 伪装

```sh
## /etc/ufw/sysctl.conf
net/ipv4/ip_forward=1

## /etc/ufw/before.rules
# *filter section for 10.0.0.0/8 and wg0 interface:
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 10.0.0.0/8 -o wg0 -j MASQUERADE
COMMIT

sudo ufw route allow in on eth0 out on wg0 from 10.0.0.0/8
```

### egress filtering

```sh
# block RFC1918 addresses going out of eth0 interfaces on your VM connected to the Internet. Add the ufw route rules to reject the traffic
sudo ufw route reject out on eth0 to 10.0.0.0/8 comment 'RFC1918 reject'
sudo ufw route reject out on eth0 to 172.16.0.0/12 comment 'RFC1918 reject'
sudo ufw route reject out on eth0 to 192.168.0.0/16 comment 'RFC1918 reject'
```

### forward

- configure ufw to forward port 80/443 to internal server hosted on LAN
- Postrouting and IP Masquerading
- configure ufw to setup a port forward

```sh
## DNAT
/sbin/iptables -t nat -A PREROUTING -i eth0 -p tcp -d {PUBLIC_IP} --dport 80 -j DNAT --to {INTERNAL_IP}:80

/sbin/iptables -t nat -A PREROUTING -i eth0 -p tcp -d {PUBLIC_IP} --dport 443 -j DNAT --to {INTERNAL_IP}:443

# To allow LAN nodes with private IP addresses to communicate with external public networks, configure the firewall for IP masquerading, which masks requests from LAN nodes with the IP address of the firewall’s external device such as eth0. The syntax is:
/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

/sbin/iptables -t nat -A POSTROUTING -s 192.168.1.0/24 ! -d 192.168.1.0/24 -j MASQUERADE

## edit /etc/ufw/before.rules
*nat
:PREROUTING ACCEPT [0:0]
# forward 202.54.1.1  port 80 to 192.168.1.100:80
# forward 202.54.1.1  port 443 to 192.168.1.100:443
-A PREROUTING -i eth0 -d 202.54.1.1   -p tcp --dport 80 -j  DNAT --to-destination 192.168.1.100:80
-A PREROUTING -i eth0 -d 202.54.1.1   -p tcp --dport 443 -j  DNAT --to-destination 192.168.1.100:443
# setup routing
-A POSTROUTING -s 192.168.1.0/24 ! -d 192.168.1.0/24 -j MASQUERADE
COMMIT

## sudo vi /etc/sysctl.conf
net.ipv4.ip_forward=1

sudo sysctl -p
sudo systemctl restart ufw

sudo ufw allow proto tcp from any to 202.54.1.1 port 80
sudo ufw allow proto tcp from any to 202.54.1.1 port 443

# Verify new settings:
sudo ufw status
sudo iptables -t nat -L -n -v
```

## nftables

- 只有先关闭 iptables 的 nat 模块，流量才能走 nft 的 nat

```sh
# 先清空规则，然后INPUT OUTPUT FORWARD全接受，如果drop会让22端口也被干掉！
iptables -F
iptables -X
iptables -Z
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
# 查询nat表所有规则
iptables -t nat -L --line-numbers
# 删除nat表POSTROUTING链规则的第一条
iptables -t nat -D POSTROUTING  1

# 保存iptables规则
iptables-save > default.rules
# 将文件default.rules发送到一台有iptables翻译nftables规则的ubantu上并输入nft命令
iptables-restore-translate -f default.rules


# 在关掉 iptables 以及 iptables 的 nat 后进入 nftables 的交互模式执行
nft

# Translated by iptables-restore-translate v1.6.1 on Tue Jul  6 16:30:39 2021
add table ip filter
add chain ip filter INPUT { type filter hook input priority 0; policy accept; }
add chain ip filter FORWARD { type filter hook forward priority 0; policy accept; }
add chain ip filter OUTPUT { type filter hook output priority 0; policy accept; }
add table ip nat
add chain ip nat PREROUTING { type nat hook prerouting priority 0; policy accept; }
add chain ip nat INPUT { type nat hook input priority 0; policy accept; }
add chain ip nat OUTPUT { type nat hook output priority 0; policy accept; }
add chain ip nat POSTROUTING { type nat hook postrouting priority 0; policy accept; }
add rule ip nat POSTROUTING oifname eth0 ip saddr 10.121.6.6 ip daddr 192.168.5.77 counter masquerade
add rule ip nat POSTROUTING oifname eth0 ip saddr 10.121.6.6 ip daddr 10.10.210.11 counter masquerade
# Completed on Tue Jul  6 16:30:39 2021

# 停止iptables服务
systemctl stop iptables.service
# 查看并确定服务是停止状态
systemctl status iptables.service
# 卸载nat模块
modprobe -v -r ip6table_nat
modprobe -v -r iptable_nat
modprobe -v -r ip_nat_ftp

# -i参数进入交互模式
nft -i
# 执行从iptables基础规则转换来的nftables规则
add table ip filter
add chain ip filter INPUT { type filter hook input priority 0; policy accept; }
add chain ip filter FORWARD { type filter hook forward priority 0; policy accept; }
add chain ip filter OUTPUT { type filter hook output priority 0; policy accept; }
add table ip nat
add chain ip nat PREROUTING { type nat hook prerouting priority 0; policy accept; }
add chain ip nat INPUT { type nat hook input priority 0; policy accept; }
add chain ip nat OUTPUT { type nat hook output priority 0; policy accept; }
add chain ip nat POSTROUTING { type nat hook postrouting priority 0; policy accept; }
add rule ip nat POSTROUTING oifname eth0 ip saddr 10.121.6.6 ip daddr 192.168.5.71 counter masquerade
add rule ip nat POSTROUTING oifname eth0 ip saddr 10.121.6.6 ip daddr 10.10.210.18 counter masquerade
# 增加测量流量规则
add rule filter INPUT counter
add rule nat POSTROUTING counter
# 查看目前的nft规则
nft list ruleset -a
```

## ACL Access Control List 访问控制列表

- 安全组 规则的集合
- 安全组规则可以自动下发到每个在安全组里面的虚拟机上，从而控制一大批虚拟机的安全策略

```sh
# 所有门关闭
iptables -t filter -A INPUT -s 0.0.0.0/0.0.0.0 -d X.X.X.X -j DROP

# 打开 ssh
iptables -I INPUT -s 0.0.0.0/0.0.0.0 -d X.X.X.X -p tcp --dport 22 -j ACCEPT

# 打开 Web
iptables -A INPUT -s 0.0.0.0/0.0.0.0 -d X.X.X.X -p tcp --dport 80 -j ACCEPT
```

## 参考

- <https://www.cyberciti.biz/tips/linux-iptables-examples.html>
