---
layout: post
title: "学习笔记--并查集"
img: himalayan.jpg # Add image post (optional)
date: 2021-01-13 11:42:00
tag: [Travel, Blogging, Mountains]
---
### 一. 概述:
#### &emsp;&emsp;并查集是一种树型的数据结构，用于处理一些不相交集合（disjoint sets）的合并及查询问题。在使用中常常以森林形式来表示。

### 二. 主要操作:
#### &emsp;&emsp;1. 初始化：把每个点所在集合初始化为其自身。
#### &emsp;&emsp;2. 查找：查找元素所在的集合，即根节点。
#### &emsp;&emsp;3. 合并：如果两个元素属于同一个集合，则将这两个元素所在的集合合并为一个集合。

### 三. 主要应用:
#### &emsp;&emsp;1. 检查图中两点是否在同一个连通子图中。
#### &emsp;&emsp;2. TODO。
