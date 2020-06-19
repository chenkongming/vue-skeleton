###注意：如果同学们不使用page-skeleton-webpack-plugin和vue-server-renderer，并且，你希望生成的骨架屏可以和页面相匹配，可以往下看！！！



###实现原理：
###给需要的dom标签设置特定类名，使用getBoundingClientRect来获取dom标签的大小和位置信息，并以此来生成一个占位符，最终生成一份“骨架屏”，当页面加载完毕，移除该“骨架屏”组件即可。因为这是在mounted周期获取元素信息，故如果元素信息不满意，需要先默认一些初始数据

###Taro骨架屏也写了一下
https://blog.csdn.net/u010214074/article/details/90120727

###github地址：
https://github.com/chenkongming/vue-skeleton
