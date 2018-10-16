---
layout: post
title: "LeetCode题解----三数之和"
img: himalayan.jpg # Add image post (optional)
date: 2018-10-16 22:08:00
tag: [Travel, Blogging, Mountains]
---
### 1.题目:
#### &emsp;&emsp;给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 。找出所有满足条件且不重复的三元组。
#### &emsp;&emsp;注意：答案中不可以包含重复的三元组。

### 2.题解: 
#### &emsp;&emsp;这道题主要注意的就是不能TLE，所以说不能三重循环暴力求解，需要使用技巧。
#### &emsp;&emsp;这里提供一个解法(参考自网上博客)：首先对数组(nums)进行排序，之后遍历整个数组，先固定一个数字(num[i])，再以双指针遍历的方式遍历i+1~nums.length-1的数组找到另外两个和它匹配的数字。
#### &emsp;&emsp;这里去除重复数组的方法是跳过重复数字，在固定数字和找另外两个数字的时候都要跳过重复数字。
#### &emsp;&emsp;通过这题要学会双指针遍历数组。