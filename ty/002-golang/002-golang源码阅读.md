# golang源码调试

dlv进行调试golang

# map实现

高效map的几种方式

https://github.com/halfrost/Halfrost-Field  参考博客实现呢 

1. hash算法 
2. 如何解决hash冲突
3. 扩容方式、是否存在缩容情况
4. 并发安全的map
   1. mutex-lock
   2. 读写分离map
   3. free-lock ==cas
   4. seg map
5. php中实现的高效map     两边数组映射呗
6. redis中如何实现的map   是如何进行扩容的呢
7. java中如何实现的map     如何正在扩容时候进行读数据就是会发生什么呢
8. golang中map如何实现的 扩容形式  并发安全map如何实现的呢
9. map插入有序设计 （根据map插入的顺序返回）
10. map读数据有序 （根据value 某一个特征返回某一个key的所有value呗）



# slice



1. 动态数组 
2. 支持常见类型呗
3. 扩容方式
4. make&append操作



## append



# channel

1. 如何支持多种数据类型的呢
2. 有缓冲和无缓冲区别呢
3. 

# atomic

原子性 

1. 原子性概念
2. 单核cpu实现原子性
3. 多核cpu实现原子性
4. 代码中如何实现原子性
5. 原子性适用场景



# mutex



1. 锁与原子性区别
2. golang锁实现方式
3. 悲观锁 乐观锁 自旋锁  饥饿模式 等待模式

# rwmutex

1. 读写锁和正常mutex锁区别

# 指针ptr



1. 正常指针ptr所占字节空间
2. unsafe.Poniter 与 其他类型可以操作运算符指针

# interface

空interface

1. 组成内容
2. 传递
3. interface与java Object 与 c语言 void类型比较 



方法interface

1. struct实现Interface 如何在运行时找到合适的struct
2. 内部组成部门
3. 值实现与指针实现区别

# defer

1. 内部数据结构组成
2. defer和return关键字在执行上的顺序



# make&&new





# panic&&recover

1. panic如何补货
2. 多协程Panic 
3. recover关键字 在什么地方起作用呢



# 值传递or引用传递

string转[]byte发生内存拷贝吗  如何禁止内存拷贝又要实现上述效果呢

1. 结构体值传递好 还是 指针传递好
2. 基本类型值传递好 还是指针传递好

1.  string转[]byte 是否发生内存拷贝 如果发生在哪里发生呗
2. []byte转string 
3. 高效转换方式

# GMP

1. GMP调度模型
2. Goroutine数据结构





# JSON



golang原生自带json序列化方式好吗？性能在哪有差异呢  如何来提升性能

json字段又是如何进行序列化的呢



1. Json序列化出现的问题
2. 关联gorm 要进行更新操作的时候转换形式
3. tag标签

# GC

1. 计数引用缺陷 如何解决  三色标记 php
2. 

# TCP

1. TCP三次握手 golang如何执行的



# Socket

1. socket实现ji

# HTTP



# 排序



# 接口可以比较吗 & 结构体可以比较吗



# -----------------------==golang==--------------------------

# 基础

1. uint不能直接相减，结果是负数会变成一个很大的uint，这点对动态语言出身的会可能坑。

2. 

3. gin框架路由是怎么实现的，具体正则怎么匹配？限流中间件怎么做
4. go的slice与数组有什么区别，slice的实现原理
5. golang协程调度，gpm模型
6. golang的channel实现，channel有缓存和无缓存
7. golang的关键字 defer、recover、panic
8. sync包里边的锁、原子操作、waitgroup之类
9. make和new区别，引用类型和非引用类型值传递之类的



## float浮点数

浮点数转换呗 NaN表示

## 字符串与[]byte相互转换，会发生内存拷贝吗



## go实现延迟队列

https://juejin.cn/post/7146641201301569566



## 变量赋值

var a []int和a := []int{}是否有区别？如果有的话，具体有什么区别？在开发过程中使用哪个更好，为什么？ 



## 结构体比较

在Go语言中，结构体是否能够比较？该如何比较两个结构体？如何比较两个接口？可以顺便查考一下代码实现。 



# 容器

1. 并发使用map除了加锁还有什么方法
2. 有对比sync.Map和加锁的区别吗



## slice底层与扩容机制



## map && sync.map



## 容器copy

Go中，如何复制切片内容？如何复制map内容？如何复制接口内容？编程时会如何操作实现。

# 并发



## GMP模型

## channel线程安全吗



## groutine 结构



## CAS具体是如何实现的



## mutex是悲观锁还是乐观锁

