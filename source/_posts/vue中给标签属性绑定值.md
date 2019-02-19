---
title: vue中给标签属性绑定值
date: 2018-10-30 10:48:00
tags:
 - vue
 - 一些坑
categories: 
  - 搭社团网页遇到的问题
---
给属性绑定值时并非
```
<img src="{{e.head}}">
```
而是
```
<img :src="bList.head">
```
