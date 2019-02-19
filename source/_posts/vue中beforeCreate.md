---
title: vue中beforeCreate
date: 2018-10-31 09:15:00
tags:
 - vue
 - 一些坑
categories: 
  - 搭社团网页遇到的问题
---
beforeCreate最好不要改动data里的数据，否则可能会出现无法监听的情况，模板中需要使用data进行渲染时，先给data默认的初始值，created之后再进行更改（如ajax）改成需要的值。