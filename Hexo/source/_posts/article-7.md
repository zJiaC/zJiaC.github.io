---
title: 日常经验备忘录
date: 2018-03-13 15:46:37
tags: [Hexo,备忘录]
categories: [Hexo]
---

# 记录个人常用的命令行指令、常用工具等：

<!--more-->

# 命令行:

1. windows系统下，由于文件夹嵌套过多，导致无法删除文件夹情况。 robocopy /MIR D:\empty-folder D:\folder-to-delete 

2. 查看端口PID CMD>netstat -ano | findstr 8080 假设为1234;kill掉这个进程 CMD>taskkill /F /PID 1234

# 常用工具:

1. Windows系统下，Nrm用于切换npm源的工具
2. Gnvm用于windows下升级node