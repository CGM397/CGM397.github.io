---
layout: post
title: "CentOS7 下 hadoop&spark 安装部署"
img: himalayan.jpg # Add image post (optional)
date: 2020-10-18 10:38:00
tag: [Travel, Blogging, Mountains]
---
### 一. Linux环境:
#### &emsp;&emsp;1. 至少准备三台Linux服务器
#### &emsp;&emsp;2. 修改主机名：`vim /etc/hostname`(永久修改)或`hostname NAME`(临时修改，关机之后失效)，分别改为master、slave1和slave2。
#### &emsp;&emsp;3. 修改hosts文件：`vim /etc/host`，将上述主机名和其ip对应起来。
#### &emsp;&emsp;4. 设置SSH实现主机之间免密登录：`ssh-keygen -t rsa -P '' -f ~/.ssh/id_dsa` 生成SSH key，然后将三个机子上的key都分别存入authorized_keys文件中，再将此文件放入三个机子中的~/.ssh目录下。最后可以用`ssh hostname`来尝试登录其他主机来验证。

### 二. 重新安装JDK:
#### &emsp;&emsp;1. 删除CentOS自带的openjdk(如果有)，使用`rpm -qa | grep java`命令得到本机上所有的java组件，然后使用`rpm -e --nodeps 上述组件名`命令删除所有组件。
#### &emsp;&emsp;2. 安装Oracle JDK：下载jdk1.8，解压缩，配置环境变量，source命令使其生效。
#### &emsp;&emsp;3. 使用`java -version`验证安装是否成功。

### 三. 安装、配置Hadoop:
#### &emsp;&emsp;1. 下载hadoop，解压缩。
#### &emsp;&emsp;2. 修改核心配置文件：core-site.xml、hdfs-site.xml、mapred-site.xml、yarn-site.xml、hadoop-env.sh、slaves/workers文件。具体配置见官网或者此[博客](https://zhuanlan.zhihu.com/p/32561305)。
#### &emsp;&emsp;3. 配置环境变量：配置HADOOP\_HOME，将\$HADOOP\_HOME/bin和$HADOOP\_HOME/sbin加入到PATH中，source使其生效。

### 四. 启动Hadoop:
#### &emsp;&emsp;1. 使用`hadoop namenode -format`命令进行初始化。
#### &emsp;&emsp;2. cd到$HADOOP\_HOME/sbin目录下(配置了PATH是不是可以不用cd到对应目录下了？)使用`./start-dfs.sh`命令启动hdfs。(启动yarn也一样)
#### &emsp;&emsp;3. 验证：输入`jps`命令查看进程，如果有master节点有NameNode和SecondaryNameNode，其他主机有DataNode，则启动成功。
#### &emsp;&emsp;4. 注意点：打开页面`master:50070`，如果其中的Live Nodes为0，可能是因为防火墙没有关闭，可以在所有机子上输入命令`systemctl stop firewalld`命令来关闭防火墙，**注意**，每次重启主机的时候可能都需要再次手动关闭防火墙。

### 五. 安装、配置Spark:
#### &emsp;&emsp;1. 下载Spark，解压缩，配置环境变量，source使其生效。
#### &emsp;&emsp;2. 修改核心配置文件($SPARK\_HOME/conf)：slaves、spark-default.conf、spark-env.sh文件。具体配置见官网或者此[博客](https://www.linuxidc.com/Linux/2018-06/152795.htm)。其中的spark-default.conf配置文件是默认的spark程序启动时使用的配置参数，可以根据实际情况设置。

### 六. 启动Spark:
#### &emsp;&emsp;1. cd到$SPARK\_HOME/sbin目录下使用`./start-all.sh`命令启动spark，如果想查看spark程序执行的历史log，可以在配置了eventLog之后，使用`./start-history-server.sh`命令启动historyServer。
#### &emsp;&emsp;2. 验证：输入`jps`命令，如果master节点上有master进程，其他节点上有worker进程，则说明启动成功。
#### &emsp;&emsp;3. 网页查看：`master:8080`：查看spark运行情况；`master:18080`: 查看spark程序执行的历史log。

### 七. 提交Spark程序:
#### &emsp;&emsp;1. 使用spark-submit命令，具体使用方法可见官网或者此[博客](https://blog.csdn.net/zylove2010/article/details/78405295)。
#### &emsp;&emsp;2. 网页查看：`master:8080`：查看spark程序运行情况；`master:18080`: 查看spark程序执行的历史log。