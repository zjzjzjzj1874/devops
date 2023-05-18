# devops
尝试一些运维相关的知识或者记录，包括Linux命令，运维基础知识等

## Network

### traceroute
Traceroute是一种网络诊断工具，用于确定数据包从源主机到目标主机的路径。 它通过发送一系列的网络探测数据包（通常是使用ICMP协议）并在每一跳上进行记录，以确定数据包经过的路径和跳数。Traceroute工具可用于查找网络连接问题、测量网络延迟和诊断网络故障。
```bash
traceroute 192.168.0.1
traceroute www.baidu.com
```
* Traceroute会发送一系列的数据包，每个数据包都带有一个逐跳时间戳（TTL），开始的TTL值通常为1。
* 数据包在网络上逐跳传输，每经过一个路由器或节点，TTL值会递增。
* 当某个数据包到达目标主机时，目标主机会返回一个ICMP响应。
* Traceroute会显示每个节点的IP地址、名称（如果可用）、节点之间的延迟和TTL值。

Traceroute输出结果将显示整个路径中每个节点的信息，包括IP地址、名称（如果可用）和延迟时间。通过分析Traceroute的输出，可以确定网络连接的路径、延迟和潜在的故障点，有助于网络故障排除和网络优化。

### 怎么在一台Ubuntu机器上查看出口IP
- 查看公网ip
```shell
# 向ifconfig.me发送请求，并返回机器的出口IP地址
curl ifconfig.me  

# 使用OpenDNS的解析器查询机器的出口IP地址
dig +short myip.opendns.com @resolver1.opendns.com 
```
- 查看内网IP
```shell
# 返回与目标IP地址1.1.1.1相关联的出口IP地址
ip route get 1.1.1.1 | grep -oP 'src \K\S+'

# 返回机器的主机名相关联的出口IP地址
hostname -I | awk '{print $1}'
```