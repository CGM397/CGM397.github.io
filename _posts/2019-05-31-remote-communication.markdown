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
#### &emsp;&emsp;使用：详见github项目，首先需要创建一个idl文件，其中有需要暴露的接口，之后再使用命令行创建idl文件对应的module包，创建方法：在命令行中输入 idlj -fall idl文件路径，具体连接方法详见github项目。
#### &emsp;&emsp;注意事项：切记，在运行服务器端之前，需要先启动ordb.exe，ORDB的作用是使客户端能够在CORBA环境中的服务器上查找和调用持久对象。启动方法：在服务器的命令行中输入 start orbd -port 8080 -ORBInitialPort 1049 -ORBInitialHost localhost，其中8080是绑定的端口，1049是初始化的端口，初始化接口只要不冲突就可以随便指定一个空闲端口。

### 3. 远程方法调用(RMI):
#### &emsp;&emsp;简介：Java提供的一种远程方法调用机制。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：需要暴露的接口需要继承Remote类，其中的方法需要抛出RemoteException；实现类需要继承UnicastRemoteObject类，构造函数需要是public并抛出RemoteException，客户端的接口需要和服务器端的接口一致。

### 4. Web Service:
#### &emsp;&emsp;简介：将接口转成WSDL文件，由客户端调用。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：可以在IDEA或者Eclipse中创建WebService服务器端和客户端，创建客户端之后可以从服务器提供的端口下载服务，如果下载失败(限制访问某文件)的话，可以在/path/jdk1.8/jre/lib/下面创建一个jaxp.properties文件(如果不存在的话)，然后写入这一行：javax.xml.accessexternalschema = all；也可以在命令行中输入如下命令来下载服务器端的服务：wsimport -s . http://localhost:8080/WebServiceTest?wsdl，其中的'-s'代表下载.java文件和.class文件，'.'指的是下载路径，为当前路径，最后的为服务器端提供的端口。

### 5. 消息队列(MQ):
#### &emsp;&emsp;简介：“消息队列”是在消息的传输过程中保存消息的容器。消息队列的主要特点是异步处理，主要目的是减少请求响应时间和解耦。可以用来进行远程方法调用。
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。

### 6. 分布式组件对象模型(DCOM):
#### &emsp;&emsp;简介：
#### &emsp;&emsp;使用：详见github项目。
#### &emsp;&emsp;注意事项：TODO。