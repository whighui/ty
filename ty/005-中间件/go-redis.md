# redis-go实现呢

如何实现一个简单 key-value 的内存数据库呢

redis有什么特点呢

1. key索引结构：采用hash，mysql采用b+树， rocksDB采用跳表作为索引
2. 丰富的数据类型：hash set zset list string stream
3. 持久化、集群、哨兵
4. 高效的内存分配  需要了解redis有哪些内存分配策略
5. 过期删除
6. 内存淘汰
7. 事件处理
8. 横向扩展-网络框架进行访问  而不是开源库
9. 

# ==c语言==



# void类型指针





# ==golang==

# interface本质

https://zhuanlan.zhihu.com/p/30749203  类似于c语言void类型 java object类型

这里边interface就是分情况呢 

1. 空的interface 也就是类似于void或者java object类型 这种底层数据结构是由eface来实现
2. 另一种就是Interface{}是由一组方法来实现 这时候底层数据结构是iface 

而实现类，分结构体实现和指针结构体实现。两种实现方法也是不一样呢，其中指针结构体效率更高一些。

参考博客 k8s大佬 非常牛逼

# golang如何实现像c语言void类型指针呢

https://i6448038.github.io/2020/03/13/unsafe-pointer/

https://cloud.tencent.com/developer/article/2213790  正常指针《========》unsafe.pointer《====》unsafe.uintptr指针

需要指针转化成结构体

需要结构体转化成指针







# ==golang正式实现redis==



# -----------------------数据结构----------------------------------



# sds字符串

## string命令

https://mp.weixin.qq.com/s/uYUQ1P8Dq1Cdknxif7lF-g   这个有关先关操作 就是非常不错呢

## bitmap命令



bitmap实现底层可以是string  或者 是long数组等  主要就是通过二进制来进行操作呢 

https://www.pch520.com/article/108   这个文章非常不错

## 内存对齐

https://eddycjy.gitbook.io/golang/di-1-ke-za-tan/go-memory-align

## c语言知识

源码中的__attribute__((__packed__))需要重点关注，结构体按照1字节对齐

1. c语言禁止内存对齐 性能是否有下降
2. golang语言如何禁止内存对齐，以及如何按照一字节对齐呢

golang中结构体存在有内存对齐，如何实现像c语言一样一字节对齐呢

## sds与c字符串区别



思考要如何实现一个字符串类型，redis sds需要支持什么特性

1. 二进制安全字符串
2. 支持append追加操作
3. 而golang如何实现呢

字符串相关又有什么命令呢





![img](https://img-blog.csdnimg.cn/20200425221532166.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmdzaGFuZ3dlaQ==,size_16,color_FFFFFF,t_70)

# list 列表



## blpop

需要了解

1. 如何阻塞客户端
2. 如何解除客户端阻塞
3. 客户端阻塞流程

# dict 哈希



# set 集合



# sortset 有序集合



# stream  流





# --------------------------命令处理生命周期----------------------

# socket网络编程



| 同步   |      |      |
| ------ | ---- | ---- |
| 异步   |      |      |
| 阻塞   |      |      |
| 非阻塞 |      |      |



首先要了解 socket阻塞和非阻塞模式  会带来什么影响

https://whiteccinn.github.io/2018/02/23/network-model/   linux下五中IO模型



1. 阻塞IO    mysql网络编程当中使用阻塞IO  采用线程池计技术来解决连接
2. 非阻塞IO
3. IO多路复用
4. 信号驱动IO模型
5. 异步IO模型



# 时间事件



# 文件事件



# 过期策略

# 内存淘汰策略



# RESP协议



# --------------------------集群、哨兵、持久化------------------



# 持久化



# 集群



# 哨兵



# 分布式锁



# --------------------------面试-----------------------------------



# 键值对数据库包含什么？

也即就是简单key-value内存数据库与redis的的对比



# 为什么还有压缩列表和整数数组类型的数据结构

整数数组和压缩列表在查找时间复杂度方面并没有很大的优势，那为什么 Redis 还会把它们作为底层数据结构呢？

1、内存利用率，数组和压缩列表都是非常紧凑的数据结构，它比链表占用的内存要更少。Redis是内存数据库，大量数据存到内存中，此时需要做尽可能的优化，提高内存的利用率。

 2、数组对CPU高速缓存支持更友好，所以Redis在设计时，集合数据元素较少情况下，默认采用内存紧凑排列的方式存储，同时利用CPU高速缓存不会降低访问速度。当数据元素超过设定阈值后，避免查询时间复杂度太高，转为哈希和跳表数据结构存储，保证查询效率。



**如果在数组上是随机访问，对CPU高速缓存还友好不？**

取决于数组大小了，如果数据空间小于CPU L1 cache，还是友好的；否则就不友好了，涉及cache line 淘汰和更新了。

# rehash过程

1. 如何rehash
2. 元素是移动还是复制
3. 热数据如何rehash
4. 冷数据如何rehash
5. rehash临界点在哪
6. rehash完成之后如何操作
7. 内存是否变为原来的2倍







# redis为什么这么快

1. 高性能IO模型 epoll accept和recv不是阻塞 监听客户端文件描述符，当有动作时候服务端调用回调函数来进行处理。多路复用机制来实现处理客户端大量请求，实现高吞吐
2. socket是长连接还是短连接
3. 并不只是单线程，单线程意指在网络处理、解析、读写处理使用单线程来处理
   1. 例如像持久化、惰性key删除、集群数据同步 是额外线程来处理
4. 多线程编程模式面临共享资源的并发访问控制问题



思考：

nety网络框架：请求一个线程，处理业务一个线程 recator模型

mysql数据库：线程池连接  单线程处理业务 。IO不是性能瓶颈，而是优化在存取的方向上



# bitmap 10亿QQ号去重 限制内存1GB





# redis 大key问题  

所谓大key 其实也就是big-key。对redis系统本身就是有什么影响呗  

遇到大key问题就是该如何解决呢



# -------------------------极客时间----------------------



不论干什么 就是希望自己坚持住呢 无论做什么事情贵在坚持吧
