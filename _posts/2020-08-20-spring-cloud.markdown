---
layout: post
title: "Spring Cloud学习笔记"
img: himalayan.jpg # Add image post (optional)
date: 2020-08-20 12:00:00
tag: [Travel, Blogging, Mountains]
---
### 一. Spring Cloud:
#### &emsp;&emsp;1. 简介：微服务框架。
#### &emsp;&emsp;2. 注意点：与Spring Boot整合时，需要解决版本对应问题。

### 二. Eureka:
#### &emsp;&emsp;1. 简介：微服务注册中心，用于服务的注册与发现。
#### &emsp;&emsp;2. server：当server端口不是8761时，需要规定defaultZone，使端口一致。
#### &emsp;&emsp;3. client：配置server的defaultZone。

### 三. Zuul:
#### &emsp;&emsp;1. 简介：网关，用于路由的映射和请求的过滤。
#### &emsp;&emsp;2. 注意点：默认设置eureka中的所有服务映射，建议关闭此设置以防暴露不需要暴露的服务，手动设置path和对应的service-id。

### 四. Spring Cloud Config:
#### &emsp;&emsp;1. 简介：统一配置中心。
#### &emsp;&emsp;2. 使用：通常和Spring Cloud Bus联合使用实现动态刷新，可以实现网关的动态路由配置。
#### &emsp;&emsp;3. server注意点：可以注册到eureka中，也可以不注册，不注册的话，其他微服务调用config server时需要给出config server地址。与Spring Cloud Bus联合使用时，需要添加消息总线支持spring-cloud-starter-bus-amqp，然后暴露bus-refresh监控端点并配置消息队列，如RabbitMQ。可以添加spring security为配置文件提供保护，此时需要为/actuator/bus-refesh端点放行。
#### &emsp;&emsp;4. client注意点：与Spring Cloud Bus联合使用时，需要添加消息总线支持spring-cloud-starter-bus-amqp并配置消息队列，如RabbitMQ。在需要刷新的类或方法上添加注释@RefreshScope。

### 五. Spring Cloud Bus:
#### &emsp;&emsp;1. 简介：基于消息队列，以广播的形式将需要通知的消息通知到各服务
#### &emsp;&emsp;2. 使用：配合Spring Cloud Config实现配置的动态刷新。使用/actuator/bus-refresh进行全局通知，使用/actuator/bus-refresh/{destination}进行定点通知。