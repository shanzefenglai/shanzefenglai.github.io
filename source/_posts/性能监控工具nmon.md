---
title: 性能监控工具nmon
date: 2019-04-15 17:24:22
tags: [性能测试,nmon]
categories: 性能测试

---

# nmon
### 检查安装环境
1、查看版本内核
```
uname -a
```

2、查看系统版本
```
cat /etc/redhat-release
```
<!--more-->
### 下载
根据系统版本下载对应版本的nmon：     
http://nmon.sourceforge.net/pmwiki.php?n=Site.Download 
CentOS7安装nmon16e_mpginc.tar.gz
nmon analyze下载：    
https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power+Systems/page/nmon_analyser
### 安装
- 安装位置/opt/nmon
- 在opt目录下创建nmon文件夹
```
[root@localhost ~]# cd /opt
[root@localhost opt]# mkdir nmon
```
- 上传nmon16e_mpginc.tar.gz到nmon目录
- 解压
```
[root@localhost nmon]# tar -zxvf nmon16e_mpginc.tar.gz
```
- 赋权限
```
[root@localhost nmon]# cd ../
[root@localhost opt]# chmod -R 755 nmon
```
- 启动
```
[root@localhost nmon]# ./nmon_x86_64_centos7
```

### 配置环境变量
- 修改启动文件名称
```
[root@localhost nmon]# mv nmon_x86_64_centos7 nmon
[root@localhost nmon]# ./nmon
```
- 添加到配置文件中
```
[root@localhost nmon]# vi /etc/profile
```
<code>PATH=$PATH:/opt/nmon/nmon<code> $PATH:后为命令的路径
<code>export PATH<code>
保存后退出
- 使配置文件立即生效
```
[root@localhost nmon]# source /etc/profile
[root@localhost nmon]# nmon   （在任何目录下执行nmon命令启动nmon）
```

### 数据采集
```
[root@localhost nmon]# nmon –f –t –r test –s 1 –c 30 -m /opt/nmon
```
|命令|说明|
|---|:--|
|-s1 | 每隔n秒抽样一次，这里为1秒|
|-c30 | 取出多少个抽样数量，这里为30，即监控=1*30/60=0.5分钟|
|-f  |按标准格式输出文件名称：<hostname>_YYMMDD_HHMM.nmon|
|-m  | 指定监控文件的存放目录，-m后跟指定目录|
|-t   |输出最耗资源的进程|
|-r test   | 监控记录的标题|
### 生成图形化报表
- 将.nmon文件转化为.csv文件
```
sort localhost_190415_1642.nmon>localhost_190415_1642.csv
```
- 将csv文件下载到本地
- 在本地解压nmon_analyser工具，打开nmon _analyser_v60.xlsm
- 在Analyser页签，点击Analyze nmon data加载csv文件
### 结束nmon运行
`ps -ef|grep nmon`
`kill -9 pid`
