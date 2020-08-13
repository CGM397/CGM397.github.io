---
layout: post
title: "回溯算法学习笔记"
img: himalayan.jpg # Add image post (optional)
date: 2020-08-13 16:22:00
tag: [Travel, Blogging, Mountains]
---
### 一. 注意点:
#### &emsp;&emsp;1. 回溯算法得到目标值之后也需要回溯，所以如果是只需要找到一个值的话，可以设置一个标记值，在return之后判断一下即可，详见 LeetCode No.37 解数独问题。

### 二. 套路:
#### &emsp;&emsp;1. 定义边界值以便return -> 寻找解空间进行遍历选择 -> 选择一个解 -> 下一步递归 -> 取消当前选择进行下一次选择