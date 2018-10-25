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
#### &emsp;&emsp;2.2. 头块的格式是“4D 54 68 64 00 00 00 06 ff ff nn nn dd dd”，其中“4D 54 68 64”是头块标记，后面紧接的4位表示头块的大小，现行的格式中头块固定为6个字节大小。“ff ff”指的是文件的格式，“nn nn”是MIDI文件中的轨道数，“dd dd”是每个4分音符tick数。
#### &emsp;&emsp;2.3. 每个轨道块的格式是由轨道头和若干事件组成的，轨道头的格式是“4D 54 72 6B xx xx xx xx”，其中“4D 54 72 6B”是轨道块标记，后面紧接的4位表示该轨道块的大小(不包括轨道头)。
#### &emsp;&emsp;2.4. 轨道块中有若干MIDI事件、非MIDI事件和系统码事件，其中非MIDI事件也叫meta事件。
#### &emsp;&emsp;2.5. 每个事件之前都会有一个delta-time，这个delta-time不同于头块里的delta-time，这里表示紧随其后的事件距离上一个事件的时间间隔，注意，如果是多轨同步，所有轨道块都是同时开始的，所以每个轨道块的第一个事件前面的delta-time都是距离开始的时间间隔。

### 3. delta-time(以tick为时间单位)
#### &emsp;&emsp;3.1. delta-time的格式：用多个字节表示，每个字节最高位是标志位(tick >= 128 ? 1 : 0)，其余7位是数值，最后一个字节的标志位为0，所以读取时只需要逐个字节地读，读到最高位是0的字节停止。
#### &emsp;&emsp;3.2. delta-time的16进制转10进制：首先将每个字节最高位设为0，将每个字节分别转成10进制，再分别乘以128的n次方(n = delta-time字节长度 - 1 - i，i为第i个字节，从0开始)。
#### &emsp;&emsp;3.3. 将delta-time转成绝对时间(秒、毫秒、微秒等)：找到命令码为“51”的meta事件，紧随其后的3个字节表示1个4分音符的微秒数，头块中的delta-time表示1个4分音符的tick数，两者相除可以得到1个tick的微秒数，再将转成10进制的delta-time数值乘以1个tick的微秒数，即可得到每个delta-time的微秒数。

### 4. MIDI事件
#### &emsp;&emsp;4.1. MIDI事件格式：通常以一个字节(大于128)的命令码开始，如果delta-time结束之后的那个字节小于128，则是缺省命令码的MIDI事件(只有数据)，沿用上个MIDI事件的命令码。命令码最常用的是8x(松开音符)、9x(按下音符)。命令码之后是对应的参数数据，8x、9x的参数都是两个字节：音符、速度(力度)。参数数据之后就是下一个事件的delta-time。
#### &emsp;&emsp;4.2. 获取音符事件就是从MIDI事件中获取。

### 5. meta事件
#### &emsp;&emsp;5.1. meta事件格式：固定开头：“ff”，紧接着就是命令码，常见的有“51”：3个字节数据，1个4分音符的微秒数；“58”：4个字节数据，节拍分子、节拍分母、节拍器时钟、1个4分音符包括的32分音符的个数；“59”：2个字节数据，升降号数(-7~-1：降号；0：c；1~7：升号)、大小调(0：大调；1：小调)，再接着是数据长度，最后是数据。
#### &emsp;&emsp;5.2. meta事件部分解析时可能会有错，但是如果meta事件都在一个轨道块中的话，对音符获取影响不大(只需要获取到必要的数据即可，比如“51”命令的参数数据)。

### 6. 系统码事件
#### &emsp;&emsp;6.1. 系统码事件格式：固定开头：“f0”，以“f7”结尾。
#### &emsp;&emsp;6.2. 因为系统码事件在MIDI事件中不常见，所以没有深究。

### 7. 音符
#### &emsp;&emsp;7.1. 通过音符的16进制数求音符的符号(音名加音阶)：假设音符是Ni，N是音名，i是音阶。公式：N = B mod 12；i = B div 12 - 1，其中B表示音符字节的10进制数。
#### &emsp;&emsp;7.2. N的10进制数值参照下表：
<table>
    <tr>
        <td>
            <pre>音名</pre>
        </td>
        <td>
            <pre>C</pre>
        </td>
        <td>
            <pre>#C</pre>
        </td>
        <td>
            <pre>D</pre>
        </td>
        <td>
            <pre>#D</pre>
        </td>
        <td>
            <pre>E</pre>
        </td>
        <td>
            <pre>F</pre>
        </td>
        <td>
            <pre>#F</pre>
        </td>
        <td>
            <pre>G</pre>
        </td>
        <td>
            <pre>#G</pre>
        </td>
        <td>
            <pre>A</pre>
        </td>
        <td>
            <pre>#A</pre>
        </td>
        <td>
            <pre>B</pre>
        </td>
    </tr>
    <tr>
        <td>
            <pre>10进制数值</pre>
        </td>
        <td>
            <pre>0</pre>
        </td>
        <td>
            <pre>1</pre>
        </td>
        <td>
            <pre>2</pre>
        </td>
        <td>
            <pre>3</pre>
        </td>
        <td>
            <pre>4</pre>
        </td>
        <td>
            <pre>5</pre>
        </td>
        <td>
            <pre>6</pre>
        </td>
        <td>
            <pre>7</pre>
        </td>
        <td>
            <pre>8</pre>
        </td>
        <td>
            <pre>9</pre>
        </td>
        <td>
            <pre>10</pre>
        </td>
        <td>
            <pre>11</pre>
        </td>
    </tr>
</table>

### 8. Java读取MIDI文件
#### &emsp;&emsp;8.1. 用FileInputStream，以字节位单位来读取。将读取到的字节存到数组中，之后处理数组即可。

### 9. MP3转MIDI文件
#### &emsp;&emsp;9.1. 可以用现有的软件来处理，比如cakewalk，widi等等。