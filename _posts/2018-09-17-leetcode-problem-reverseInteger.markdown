---
layout: post
title: "LeetCode题解----反转整数"
img: himalayan.jpg # Add image post (optional)
date: 2018-09-17 23:43:00
tag: [Travel, Blogging, Mountains]
---
### 1.题目: 给定一个 32 位有符号整数，将整数中的数字进行反转。

### 2.题解: 这题本身是一道容易题，但是需要注意的有两点
#### &emsp;1.Math.abs()的参数和返回值都是int，所以不可以处理long！
#### &emsp;2.看似简单的负号‘-’竟然也是不可以在后面的数类型的范围内溢出的，也就是说如果x是int类型，那么-x也不能超出int类型范围，如果超出，则还是显示x本身(其实int类型的实例也就只有一个，- 2的31次方)。