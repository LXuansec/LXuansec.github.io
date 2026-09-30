---
title: "CMake个人使用指南"
date: 2026-09-30T17:00:00+08:00
draft: true
categories: ["杂谈"]
tags: ["CMake", "C++", "构建工具"]
summary: "记录 CMake 构建工程的常用范式与原理"
---

## 1. CMake 工具

工程的自动化编译工具

## 2. 简单工程的编译范式

对于简单的单CMakeList.txt编译范式应如下：
```cmake
#设置基础信息

#cmake的最低需求版本
cmake_minimum_required(VERSION 3.16)
#项目名字
project(MyProject)
```

### 2.1 project()

project() 用于声明当前 CMake 工程，并初始化项目名、源码路径、构建路径、版本等相关变量。

用于设置工程名字，同时会对Cmake系统内部的一些固有变量赋值，例如：


project() 默认还会启用常见编程语言，一般是 C 和 CXX， 例如：
```cmake
project(MyProject LANGUAGES CXX)
```