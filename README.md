# 概念
## iptables
> iptables，一个运行在用户空间的应用软件，通过控制Linux内核netfilter模块，来管理网络数据包的流动与转送。iptables的操作需要用到超级用户的权限，要通过表（table）链（chain） 规则（rule/target）确定。

## 表（table）
> raw：高级功能，如：网址过滤。

> filter：包过滤，用于防火墙规则。

> nat：地址转换，用于网关路由器。

> manger：数据包修改（QOS），用于实现服务质量。

> security：

## 链（chain）
> INPUT：处理输入数据包。
> 
> OUTPUT：处理输出数据包。
> 
> PORWARD：处理转发数据包。
> 
> PREROUTING：用于目标地址转换（DNAT）。
> 
> POSTOUTING：用于源地址转换(SNAT)。

## 规则（rule/target）
> ACCEPT：接收数据包。
> 
> DROP：丢弃数据包。
> 
> REDIRECT：重定向、映射、透明代理。
> 
> SNAT：源地址转换。
> 
> DNAT：目标地址转换。
> 
> MASQUERATE：IP伪装（NAT），用于ADSL。
> 
> LOG：日志记录。

## 使用方法
> man iptables
> 
> iptables -h

# 示例
## 查看规则 
> 1. 常规查看：iptables -t 表名 -L
> 2. 详细查看：iptables -t 表名 -v -L
> 3. 查看标号：iptables -t 表名 -L --line-numbers

## 删除规则
> 1. 根据标号删除：iptables -t 表名 -D 链名 标号
> 2. 删除所有：iptables -t 表名 -F
>
 
## filter表添加规则
> 如过滤 mysql 3306端口，只允许1.1.1.1访问
>
```
1. 使用追加 -A
iptables -t filter -A INPUT -p tcp --dport 3306 -j DROP
iptables -t filter -A INPUT -s 1.1.1.1 -p tcp --dport 3306 -j ACCEPT
2. 使用追加 -A 和 插入 -I
iptables -t filter -A INPUT -s 1.1.1.1 -p tcp --dport 3306 -j ACCEPT
iptables -t filter -I INPUT 2 -p tcp --dport 3306 -j DROP
```

## nat表添加规则
> 如docker bridge网络模式，访问外网

```
iptables -t nat -A POSTROUTING -s 172.17.0.0/24 -j MASQUERADE
```













