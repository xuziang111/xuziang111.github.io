---
title: hexo中加载本地图片
date: 2018-09-29 20:21:32
tags:
    - hexo
---
1. 首先把blog（hexo）目录下的_config.yml里的psot_asset_folder:设置为true

2. 在blog（hexo）目录下执行:
```
npm install hexo-asset-image --save
```
3. 在blog（hexo）目录下Git Bash Here，运行hexo n "博客名"来生成md博客时，会在_post目录下看到一个与博客同名的文件夹。

4. 将想要上传的图片先扔到文件夹下，然后在博客中使用markdown的格式引入图片：
```
![图片加载不出时替代名字](图片名.jpg)
```
5. 然后，使用hexo g部署即可。