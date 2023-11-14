# 学习链接
linux学习视频[链接](https://www.bilibili.com/video/BV1n84y1i7td?p=4&vd_source=7664b55184fd63da03a03ef6c9be4310)
# 操作系统概述
操作系统是系统硬件与软件的桥梁，操作系统能通过相关操作去调度硬件资源。

主流PC操作系统：Windows,Macos,Linux。其中Linux在服务器领域是最主流的操作系统。
# 初识Linux
## 1. Linux 内核
Linux的内核免费且开源，即Linux源代码每个人都能去获取且做出自己的修改。
获取网址[链接](https://www.kernel.org/)。
## 2. Linux发行版
Linux有很多版本，每个人都可以去创造一个属于自己的Linux操作系统。
因为内核开源的原因，所以很多企业和个人都会对Linux内核做出改变且集成系统级程序。
操作系统 = 内核 + 系统级程序。
在Linux内核之上封装了系统级程序便是Linux发行版，其中用户不能直接使用内核，只能通过应用程序使用。
# 安装VMware WorkStation虚拟化软件
VMware下载地址[链接](https://www.vmware.com/cn/products/workstation-pro.html)。
# VMware里安装CentOS系统
CentOS官网下载[链接](https://vault.centos.org/)。
各个版本下载指南[链接](https://blog.51cto.com/u_15294985/2996187)。
# 远程连接Linux操作系统
## 1. 图形化和命令行
两种使用操作系统的形式。
## 2. 命令行与FinalShell
在linux系统中，命令行的使用为主流。
通过VMware软件使用Linux系统会带来许多不便，选择FinalShell操控linux系统。
Finalshell作为一款第三方软件，可以远程连接Linux系统。
为何要使用命令行呢？理由如下:
![](Pasted%20image%2020231112105657.png)
## 3. 安装FinalShell
下载官网[链接](https://www.hostbuf.com/)
## 4. Win系统FinalShell连接Linux
远程连接Linux[链接](https://blog.csdn.net/SleepingGoat/article/details/122007491?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1-122007491-blog-109636194.235%5Ev38%5Epc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1-122007491-blog-109636194.235%5Ev38%5Epc_relevant_sort_base1&utm_relevant_index=2)
虚拟机重启后IP地址可能发生改变。
获得Linux主机的IP地址命令是``ifconfig``
注意在远程连接时，用户名要到VMware软件终端看一下。

扩展--WSL配置Ubuntu
扩展--虚拟机快照
# Linux基础学习
## 1. Linux目录结构
Linux系统只有一个根目录，且根目录用``"/"``表示。
除去第一个 "/"外，后面的"/"都代表层级关系。
示例如下：
![](Pasted%20image%2020231112113407.png)
## 2. Linux命令入门
### 2.1. Linux命令基础
Linux命令通用格式如下:
![](Pasted%20image%2020231112114305.png)
### 2.2. ls 命令入门
直接使用 ls 命令 ，它的作用是``以平铺的方式列出当前工作目录（默认是Home）下的内容（文件或是文件夹）。``
每一个用户都有一个自己的Home目录。
Home目录的位置是``"/Home/用户名"``
Linux系统中的Home文件夹类似于windows里面的``C:\用户\admin``文件夹。
Linux系统刚开始的默认工作目录就是Home目录。
### 2.3. ls命令的参数和选项
```Linux
ls -a [Linux 路径]

-a 的作用是列出所有文件（即all的意思），包括隐藏文件或文件夹

其中Linux中以 . 开头的文件都是隐藏文件
```

```Linux
ls -l [Linux路径]

-l 的作用是以列表的形式列出内容，并且展示更多信息

与直接使用 ls 命令不同的是 -l 格式的展示形式变了，信息输出也更多了
```

```Linux
ls -l -h [Linux路径]

-h 的作用是以更加人性化的形式去显示文件大小

-h 单独使用没有效果 要与 -l 搭配使用
```

```Linux
组合使用命令
ls -la [Linux路径]
ls -lh [Linux路径]
ls -lah [Linux路径]
```
### 2.4. 目录切换相关命令(cd/pwd)
```Linux
cd(change directory)
cd [工作路径]
cd / 切换到根目录
cd 切换到Home目录
其中 cd 命令没有选项 只有参数
```

```Linux
(print work directory)
pwd 打印当前工作目录

其中 pwd 命令没有选项，没有参数
```
