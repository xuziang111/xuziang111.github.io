---
title: 'cropper.js的预览功能（preview）如果在渲染时，元素为display:none,就会无法预览。'
date: 2018-09-30 14:12:00
tags:
- cropperjs
- 一些坑
categories: 
  - 搭社团网页遇到的问题
---
cropper.js的预览功能（preview）如果在渲染时，元素为display:none,就会无法预览。
改成与按钮绑定，点击时display:none变为display:block,这时进行渲染就可以了。