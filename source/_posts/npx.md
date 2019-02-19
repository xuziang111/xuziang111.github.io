---
title: npx
date: 2018-11-17 22:06:27
tags:
  - npm
categories: 
  - 前端
---
npx 会自动查找当前依赖包中的可执行文件，如果找不到，就会去 PATH 里找。如果依然找不到，就会帮你安装。
例如
```
npx webpack
```