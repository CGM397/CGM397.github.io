---
layout: post
title: "LeetCode题解----电话号码的字母组合"
img: himalayan.jpg # Add image post (optional)
date: 2018-10-17 23:02:00
tag: [Travel, Blogging, Mountains]
---
### 1.题目:
#### &emsp;&emsp;给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
#### &emsp;&emsp;数字所对应的字母参照拼音九键。

### 2.题解：
#### &emsp;&emsp;本题重点就是利用递归求出所有组合。首先先将所有数字对应的字母序列放在一个List中，然后再递归求解。
#### &emsp;&emsp;递归的边界是一个数字对应的所有字母都已经被遍历，之后是循环体，这里要记得在调用自身(递归)之后，要“撤销”之前的操作。