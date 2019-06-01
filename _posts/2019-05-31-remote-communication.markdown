---
layout: post
title: "分布式系统远程调用学习笔记"
img: himalayan.jpg # Add image post (optional)
date: 2019-05-31 21:33:00
tag: [Travel, Blogging, Mountains]
---
### 1. 远程过程调用(RPC):
#### &emsp;&emsp;简介：RPC是由Sun发明的远程过程调用协议，是第一种真正的分布式应用模型。
#### &emsp;&emsp;使用：TODO。
#### &emsp;&emsp;注意事项：TODO。

### 2. 公共对象请求代理体系结构(CORBA):
#### &emsp;&emsp;简介：是由OMG组织制订的一种标准的面向对象应用程序体系规范。
#### &emsp;&emsp;使用：首先需要创建一个idl文件，其中有需要暴露的接口，之后再使用命令行创建idl文件对应的module包，创建方法：在命令行中输入 idlj -fall idl文件路径，具体连接方法详见github项目。
#### &emsp;&emsp;注意事项：切记，在运行服务器端之前，需要先启动ordb.exe，启动方法：在命令行中输入 start orbd -port 8080 -ORBInitialPort 1049 -ORBInitialHost localhost，其中8080是绑定的端口，1049是初始化的端口，初始化接口只要不冲突就可以随便指定一个空闲端口。

### 3. 远程方法调用(RMI):
#### &emsp;&emsp;简介：Java提供的一种远程方法调用机制。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。

### 4. Web Service:
#### &emsp;&emsp;简介：将接口转成WSDL文件，由客户端调用。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。

### 5. 消息队列(MQ):
#### &emsp;&emsp;简介：“消息队列”是在消息的传输过程中保存消息的容器。消息队列的主要特点是异步处理，主要目的是减少请求响应时间和解耦。可以用来进行远程方法调用。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。

### 6. 分布式组件对象模型(DCOM):
#### &emsp;&emsp;简介：
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。