# VMware与服务器实验规范

## 职责
指导VMware、Windows Server、Ubuntu及Windows
客户端的网络实验，不负责总体地址规划。

## 环境检查
确认：
- VMware产品与版本
- 虚拟机操作系统与版本
- 虚拟机启动状态
- 虚拟网卡及连接模式
- IP、掩码、网关、DNS
- 现有服务与配置
- 快照、备份和回滚条件

历史实验配置仅作为线索，
必须重新检查当前环境。

## VMware网络模式
Bridged：连接到外部二层网络的桥接模式。
NAT：通常通过宿主机的NAT网络访问外部。
Host-only：通常用于宿主机与虚拟机内部通信。

具体通信能力由实际网络配置决定。

## Windows本地状态读取
CMD：
ipconfig /all
route print

PowerShell：
Get-NetIPConfiguration
Get-DnsClientServerAddress
Get-NetRoute

## Ubuntu本地状态读取
ip -br addr
ip route
resolvectl status

命令不可用时先检查系统环境，
不要直接安装或修改配置。

## 主动DNS查询
nslookup example.com
getent hosts example.com

以上查询可能产生外部DNS请求，不属于本地状态读取。
主动DNS查询遵循SKILL.md的L2授权规则及明确批准的目标范围。
getent hosts也可能使用本地缓存或其他名称解析来源，仍按主动查询管理。

## Windows Server实验
支持：
- 静态IP与DNS
- DNS服务器角色
- 正向、反向查找区域
- DHCP作用域
- Active Directory域服务
- 域用户、组及客户端加入域

实验环境的服务配置变更通常遵循SKILL.md的L2规则；
生产环境配置修改及其他高风险变更遵循L3规则。

## DNS验证
1. 检查服务器地址
2. 检查服务状态
3. 检查客户端DNS指向
4. 检查目标记录
5. 发起查询
6. 分析响应
7. 记录证据

## DHCP验证
1. 检查服务与作用域
2. 检查地址池及排除范围
3. 检查客户端租约
4. 检查网关与DNS选项
5. 对照预期结果

租约释放与更新可能中断网络，
必须事先说明影响并取得授权。

## 域登录验证
检查DNS、域控制器解析、域加入状态、
账户身份、时间同步及必要服务。

域用户登录成功不代表组策略全部生效。

## 结束标准
记录实际操作、输出、验证状态、
异常、回滚信息及下一步任务。

不得因命令执行完成就宣布实验成功。
