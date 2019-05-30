---
layout: post
title: "Dart学习笔记"
img: himalayan.jpg # Add image post (optional)
date: 2019-05-30 23:09:00
tag: [Travel, Blogging, Mountains]
---
### 1. 简介([百度百科](https://baike.baidu.com/item/DART/22500518?fr=aladdin)):
#### &emsp;&emsp;Dart是谷歌开发的计算机编程语言，它被用于web、服务器、移动应用和物联网等领域的开发。它是宽松开源许可证（修改的BSD证书）下的开源软件。
#### &emsp;&emsp;Dart是面向对象的、类定义的、单继承的语言。它的语法类似C语言，可以转译为JavaScript，支持接口(interfaces)、混入(mixins)、抽象类(abstract classes)、具体化泛型(reified generics)、可选类型(optional typing)和sound type system。

### 2. 安装和开发环境配置:
#### &emsp;&emsp;安装：到[官网](https://dart.dev/get-dart)上下载SDK并配置环境变量(将bin添加到Path中)。
#### &emsp;&emsp;开发环境配置：可选IDEA或者Android Studio，如果选择IDEA，需要安装Dart插件

### 3. 创建Demo(在IDEA中)
#### &emsp;&emsp;创建：File->New->Project->Dart，之后可以选择不同的Demo，比如web demo，app demo和command-line demo等，我先选择了web demo，但是发现并不能运行。。。修改了几次pubspec.yaml也没用，就放弃了。转而创建一个command-line demo，就是单纯跑函数方法等的demo，适合熟悉语法。创建之后需要在idea中打开终端(terminal)，运行pub get来获取需要的依赖。
#### &emsp;&emsp;运行：点击run即可。

### 4. 基本语法
#### &emsp;&emsp;TODO