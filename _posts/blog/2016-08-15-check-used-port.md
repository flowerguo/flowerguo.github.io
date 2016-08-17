---
layout:     post
title:      在windows下查看占用端口的程序
description: 在windows下查看占用端口的程序
categories: blog
tags: 实用操作
---

转自 <a target="_blank" href="http://www.cnblogs.com/lxconan/archive/2016/01/11/5119972.html">传送门</a>

在运行命令或者程序时发现端口被其他进程占用了，如何找到被占用端口的进程呢？（比如端口4000被占用）

1、在命令行下查看各个端口被占用的情况：
     
netstat -ano

     -a:  显示所有链接和侦听端口;
     -n:  以数字形式显示地址和端口号而不会去尝试进行外部地址解析，能够显著的提高执行速度
     -o:  显示拥有与每一个链接关联的 PID。其实他还有一个 fancy 的参数 -b 可以直接拿到与指定链接关联的可执行程序的名称。但是这个参数需要管理员权限！
     
     由上可看到是PID为 2620 的进程占用了4000端口。

![img](/images/blog/checkport1.png)

2、查看占用端口的进程是什么
    
 tasklist /svc /FI "PID eq 2620"

     /svc:  如果这个进程是一个 Windows 服务的话同时显示这个服务的名称；
     /FI:  使用筛选器对结果进行筛选。
     

![img](/images/blog/checkport2.png)

3、由上得知占用端口的进程，停止服务。

