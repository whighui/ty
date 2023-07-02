# socket

socket是套接字，是对tcp和upd协议的标准对外封装



## socket



## bind



## listen



## accept



## write



## read



## close





# IO

了解同步处理和异步处理 阻塞和非阻塞等关系 所以就是在这里就是正确的呗

## 阻塞IO实现

| 客户端                      | 内核态  | 服务端                            |
| --------------------------- | ------- | --------------------------------- |
|                             |         | socket 创建服务端文件描述符fd     |
| socket 创建客户端socket     |         | bind     绑定端口和地址           |
|                             |         | listen   监听端口和地址           |
| connect tcp三次握手建立连接 |         | accept  等待连接 正常情况下是阻塞 |
| \|-->write                  | DMA技术 | read  <---------\|                |
| \|                          |         | 进程处理           \|             |
| \|--read                    |         | write ----- ----\|                |
| close                       |         | close                             |
|                             |         |                                   |



## 非阻塞IO实现

## IO多路复用实现

https://blog.csdn.net/Jmilk/article/details/105916184   epoll等仙姑

## 信号驱动IO

## 异步IO



## DMA和mmap

https://blog.csdn.net/Rong_Toa/article/details/115048648



# MakeFile

# CmakeList

