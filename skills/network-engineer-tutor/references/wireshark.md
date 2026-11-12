# Wireshark抓包与协议分析

## 职责

负责网络抓包准备、过滤器使用、协议字段分析、
实验验证和证据整理。

覆盖ICMP、ARP、DNS、DHCP、TCP、
HTTP、HTTPS及TLS等常见协议。

## 抓包前检查

确认：

- 操作系统与Wireshark版本
- 网卡名称及IP地址
- 抓包权限与驱动
- 目标和授权范围
- 测试流量及预期结果
- 数据敏感性
- 抓包保存位置

不得假定Npcap或Linux抓包权限已配置。

根据实际通信路径选择正确网卡。
必要时区分物理网卡、虚拟网卡和回环接口。

混杂模式不是所有抓包任务的必要条件，
也不意味着能够捕获交换网络中的全部流量。

## 工作流程

1. 确认实验目标
2. 检查网卡及抓包权限
3. 明确授权测试范围
4. 选择网卡及必要的捕获过滤器
5. 开始抓包
6. 发起测试流量
7. 停止抓包
8. 应用显示过滤器
9. 找到请求与响应
10. 分析关键协议字段
11. 对照预期结果
12. 保存必要证据

实际抓包和主动测试必须符合SKILL.md授权规则。

## 捕获过滤器与显示过滤器

### 捕获过滤器

捕获过滤器在抓包开始前设置，
用于控制实际捕获哪些报文。

常见示例：

```text
icmp
icmp6
host 192.0.2.10
port 53
udp port 53
tcp port 80
tcp port 443
udp port 443
udp port 67 or udp port 68
```

以上采用libpcap/BPF过滤语法。

### 显示过滤器

显示过滤器用于筛选已经捕获的报文。

常见示例：

```text
icmp
icmpv6
arp
dns
dhcp
tcp
udp
tls
http
ip.addr == 192.0.2.10
tcp.port == 443
udp.port == 443
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

192.0.2.10是文档示例地址。

DHCP显示过滤器在不同Wireshark版本中
可能存在协议字段名称差异。
遇到过滤器无法识别时，应检查当前版本
的协议字段列表，不得直接认定报文不存在。

捕获过滤器与显示过滤器的语法和作用不同，
不得混用。

## ICMP分析

检查：

- 源和目的地址
- Type、Code
- Identifier、Sequence Number
- 请求和响应的对应关系
- 实际测得的往返时间

ICMPv4：
- Echo Request：Type 8
- Echo Reply：Type 0

ICMPv6：
- Echo Request：Type 128
- Echo Reply：Type 129

以上Type编号分别适用于对应协议版本。

分析前必须确认报文属于IPv4还是IPv6。

没有捕获Echo Reply时，
应检查目标可达性、防火墙策略、
抓包接口及捕获时机。

不得仅凭缺少响应认定目标主机离线。

## ARP分析

检查：

- 请求方MAC和IP
- 目标IP
- ARP Request
- ARP Reply
- 地址解析结果

区分ARP请求、应答和实际IP通信。

不能仅凭ARP请求没有出现在当前抓包中，
就认定网络设备故障。

## DNS分析

检查：

- 查询名称
- 查询类型
- 事务ID
- 响应码
- Answer区域
- TTL
- 查询与响应的对应关系

重点识别：

- A与AAAA查询
- NXDOMAIN
- SERVFAIL
- NOERROR
- 超时和重传

注意DNS缓存、hosts文件、
DoH、DoT等名称解析方式。

dns过滤器不一定能够显示加密DNS的实际查询内容。

需要区分DNS查询成功、
DNS服务器正常运行及实际报文成功往返。

## DHCP分析

DHCPv4初始地址分配通常遵循DORA：

```text
Discover → Offer → Request → ACK
```

检查：

- 客户端MAC地址
- Transaction ID
- 客户端请求地址
- DHCP服务器标识
- 分配地址
- 租约时间
- 网关及DNS选项

DHCPv4常用UDP端口：
- Server：67
- Client：68

DHCPv6使用不同的消息交互机制。
有状态地址配置的常见交互包括：

```text
Solicit → Advertise → Request → Reply
```

DHCPv6还支持无状态信息配置等其他流程，
不能将上述消息序列视为所有DHCPv6通信的固定流程。

DHCPv6常用UDP端口：
- Server：547
- Client：546

### DHCP抓包注意事项

客户端已有有效租约时，
可能直接续租或重新绑定，
不一定重新执行完整的DORA流程。

没有捕获Discover或Offer，
不能直接认定DHCP服务故障。

应结合客户端租约、服务端作用域、
抓包接口及捕获时机判断。

租约释放与更新可能中断网络，
必须事先说明影响并取得授权。

## TCP分析

检查：

- 源和目的地址及端口
- SYN、ACK、FIN、RST
- 序列号和确认号
- 接收窗口
- 重传
- 超时
- 连接建立与释放

### 三次握手

```text
1. SYN
2. SYN-ACK
3. ACK
```

检查序列号与确认号是否对应。

### 四次挥手

典型关闭过程：

```text
1. FIN
2. ACK
3. FIN
4. ACK
```

实际关闭过程可能因同时关闭、
延迟确认等情况有所不同。

### 异常分析

重点检查：

- TCP Retransmission
- Duplicate ACK
- RST
- Zero Window
- 连接超时

不凭单个异常报文直接断定根因。

## HTTP与HTTPS分析

### HTTP

重点检查：

- 请求方法
- 请求URI
- Host
- 状态码
- 请求与响应
- 明文数据可见性

### HTTPS

重点检查：

- TCP连接（适用于TCP承载的HTTPS）
- TLS握手
- 加密通信
- 证书及握手相关信息
- 应用数据可见性

HTTP明文通信与HTTPS加密通信
应分别抓包并比较。

不能因为HTTPS应用数据不可直接阅读，
就认定通信失败。

HTTP/3通常基于QUIC和UDP，
不能只依靠TCP 443过滤器分析全部HTTPS流量。

## TLS分析

重点检查：

- ClientHello
- ServerHello
- 密钥协商相关信息
- 加密参数
- 握手完成情况
- 加密应用数据

TLS 1.3中，部分握手内容在
ServerHello之后会被加密。

证书等信息的可见性取决于握手阶段、
协议扩展和实际抓包条件。

没有密钥日志时，
通常不能直接读取TLS 1.3加密应用数据。

未经授权不得获取或使用他人的会话密钥。

## 隐私要求

PCAP可能包含：

- 凭据
- 会话信息
- 内部地址
- DNS查询
- 设备标识
- 私人数据

默认只整理必要字段。

未经批准不上传原始PCAP至公开仓库。

分享截图前检查：

- IP地址
- MAC地址
- 用户名
- 域名
- 认证信息
- 会话数据

保留原始证据时，
不得擅自覆盖或删除。

## 证据与实验记录

记录：

- 实验日期
- 操作系统及Wireshark版本
- 抓包网卡
- 捕获过滤器
- 显示过滤器
- 测试目标
- 报文编号
- 时间
- 关键协议字段
- 实际结果
- 异常及排查过程

没有真实报文时标记待验证。

明确区分实际观察、用户自述、
推断和待验证事项。

不得编造报文编号、抓包结果或实验结论。
