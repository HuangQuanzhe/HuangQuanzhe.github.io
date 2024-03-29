# TCP问题定位总结

## 前言
传输控制协议（TCP，Transmission Control Protocol）是为了在**不可靠的互联网络**上提供可靠的端到端字节流而专门设计的一个传输协议。  
1. TCP负责既要足够快地发送数据报，以便使用网络容量，但又不能引起网络拥塞。
2. TCP超时后，要重传没有递交的数据报。
3. 即使被正确递交的数据报，也可能存在错序的问题，TCP必须把接收到的数据报重新装配成正确的顺序。  

基于TCP/IP的应用层协议：
HTTP：
NFS：网络文件系统协议

服务端都很正常，服务正常，CPU使用率正常，内存使用正常，TCP连接数正常，应用层一切正常。那么我们有理由怀疑，TCP层出现了问题。比如：  

1. 频繁或者说定期出现丢包导致超时？(案例1)
2. 拥塞控制算法预测的值不准？（案例1)
3. TCP报文出现乱序？(案例3)

## 常用的网络定位工具 tcpdump 与 wireshark
tcpdump -i xxx -host xxx.xxx.xxx.xxx -w debug.pcap  

![正常图]()  
![异常图]()  

我们通过wireshark工具读取抓包文件，在工具的帮助下可以一眼看出网络存在异常。这是分析网络问题的一个通用方法。

## 案例1 同VPC内使用TCP协议进行数据传输速率极慢
场景：服务器A向服务器B请求数据，数据传输非常慢。   
跟踪TCP流进行分析
丢包
快速重传
重传
超时等待
拥塞窗口



### 案例1-1 链路丢包

### 案例1-2 网卡丢包

### 案例1-3 软件限制丢包 TC流量控制

## 案例2 网传百度网盘限速手段
场景：百度网盘下载文件不充会员速度非常慢

## 案例3 服务连接redis出现Connection Reset
场景：服务端请求redis数据，出现ConnectionReset。服务抛出异常，无法取到缓存数据，请求直接打到下级接口或者数据库。


## 案例4 拥塞控制算法不准导致的吞吐量缺陷

## 问题