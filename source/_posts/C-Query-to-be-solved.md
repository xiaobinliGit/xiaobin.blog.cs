---
title: C++ Query to be solved
date: 2017-09-18 22:03:38
categories:
  - 技术日志
  - C++
tags:
  -C++
---
### 摘要: C++11 疑惑(解惑中)
<!--more-->
最近开始C++项目，接触C++11特性的代码，相比之前99的功能强大了很多，但很多用法不明，也晦涩了很多。先在此记录罗列下，接下来需要逐步理解透彻
## 左值、右值、将亡值

## decltype+auto用法
1.auto忽略顶层const，decltype保留顶层const;
2.对引用操作，auto推断出原有类型，decltype推断出引用;
3.对解引用操作，auto推断出原有类型，decltype推断出引用;
4.auto推断时会实际执行，decltype不会执行，只做分析

## 模板元编程

## typename
1.C++11 模板中尽量用typename来分辨具体类型

## 匿名函数
1. 非常方便的一种表达方式

## constexpr/nullptr

## 