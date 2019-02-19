---
title: 基于jquery图片懒加载
date: 2019-02-19 10:01:00
tags:
 - 懒加载
 - jquery
categories: 
  - 搭社团网页遇到的问题
---
对img和div的背景图片进行懒加载。
在data-original写入真正的链接。
html
```
<div data-original="example1.jpg"></div>
<img data-original="example2.jpg">
```
javascript
```
// 注意: 需要引入jQuery
    (function() {
        // 获取window的引用:
    var $window = $(window);
     // 获取包含data-original属性的img，并以jQuery对象存入数组:
    var lazyImgs = $('img[data-original]')
	var xxx=[]
	$('img[data-original],div[data-original]').each(function(index,element){
		xxx.push($(this))
	})
    // 定义事件函数:
    var onScroll = function() {
        // 获取页面滚动的高度:
        var wtop = $window.scrollTop();
         // 判断是否还有未加载的img:
        if (xxx.length > 0) {
            // 获取可视区域高度:
            var wheight = $window.height();
            // 存放待删除的索引:
            var loadedIndex = [];
            // 循环处理数组的每个img元素:
            $.each(xxx, function (index, i) {
                // 判断是否在可视范围内:
                if (i.offset().top - wtop < wheight) {
                    //区分img与div元素区别
					if(i[0].tagName === 'IMG'){
                        //设置img的src属性
						i.attr('src', i.attr('data-original'));
					}else if(i[0].tagName === 'DIV'){
                        //设置div背景图片
						i.css("background-image","url("+i.attr('data-original')+')')
					}
                    // 添加到待删除数组:
                    loadedIndex.unshift(index);
                }
            });
            // 删除已处理的对象:
            $.each(loadedIndex, function (i,index) {
                xxx.splice(index, 1);
            });
        }
    };
    //进入页面先执行一次
    onScroll();
    //绑定scroll事件
    $(window).scroll(onScroll);
})()
```