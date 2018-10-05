---
layout: post
title: "MIDI文件学习笔记"
img: indonesia.jpg # Add image post (optional)
date: 2018-10-05 20:46:00
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
tag: [Travel, Indonesia, Mountains]
---
### 1. MIDI(Musical Instrument Digital Interface)概述
#### &emsp;&emsp;1.1. MIDI是编曲界最广泛的音乐标准格式，可称为“计算机能理解的乐谱”。(来自百度百科——[MIDI](https://baike.baidu.com/item/MIDI/217824?fr=aladdin))

### 2. MIDI文件格式
#### &emsp;&emsp;2.1. 一个MIDI文件格式是由一个头块和若干个轨道块组成的。
#### &emsp;&emsp;2.2. 头块的格式是“4D 54 68 64 00 00 00 06 ff ff nn nn dd dd”，其中“4D 54 68 64”是头块标记，后面紧接的4位表示头块的大小，现行的格式中头块固定为6个字节大小。“ff ff”指的是文件的格式，“nn nn”是MIDI文件中的轨道数，“dd dd”是每个4分音符delta-time节奏数。
#### &emsp;&emsp;2.3. 每个轨道块的格式是由轨道头和MIDI事件组成的，轨道头的格式是“4D 54 72 6B xx xx xx xx”，其中“4D 54 72 6B”是轨道块标记，后面紧接的4位表示该轨道块的大小(不包括轨道头)。

### 3. MIDI事件
#### &emsp;&emsp;3.1 待学习。

### 4. Java读取MIDI文件
#### &emsp;&emsp;4.1 用FileInputStream，以字节位单位来读取。将读取到的字节存到数组中，之后处理数组即可。

### 5. MP3转MIDI文件
#### &emsp;&emsp;5.1 可以用现有的软件来处理，比如cakewalk，widi等等。