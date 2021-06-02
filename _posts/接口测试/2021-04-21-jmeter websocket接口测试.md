---
layout: post
title:  jmeter websocket接口测试
category: 接口测试
tags: [websocket接口测试,jmeter]
---
# Jmeter安装插件

以下插件都放到 `\apache-jmeter-5.4.1\lib\ext`
[JMeter WebSocket Samplers](https://bitbucket.org/pjtr/jmeter-websocket-samplers/downloads/)
[jetty-http](http://mvnrepository.com/artifact/org.eclipse.jetty/jetty-http)
[jetty-io](http://mvnrepository.com/artifact/org.eclipse.jetty/jetty-io)

# 简单示例
![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421112456089-684144659.png)
![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421112649609-2011335098.png)
![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421112743828-598738239.png)

![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421112826285-1752103706.png)


# 持续接收数据
**遇到的问题：**
1. 如何取上一个接口返回的数据作为当前接口的参数？ - 解决方案：正则表达式提取器
![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421150252148-1137389806.png)
当前接口调用：
`"user_id":${user_id},`

2. 如何持续获取接口返回的数据？  
2.1 仅接收数据不发送数据 - 取样器：websocket single read sampler
2.2 发送数据 - use existing connectionn
![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421145642541-538699908.png)

3. 接收数据报错 `WebSocket I/O error: end of stream`
...根据[WebSocket I/O error: end of stream
](https://bitbucket.org/pjtr/jmeter-websocket-samplers/issues/71/websocket-i-o-error-end-of-stream)这篇文章地下的回答，是服务器无法处理所以主动断开了连接
因此加了一个固定定时器：5000ms接收一次数据，报错的概率小了很多

4. 如何主动的（持续的）接收数据？ 
按理说应该加一个判断， 服务端返回数据为空，就停止接收，这里简单加了一个循环控制器。

![](https://img2020.cnblogs.com/blog/826848/202104/826848-20210421181239253-1205068134.png)



参考：
[插件下载原文 ：JMeter测试WebSocket的经验总结](https://blog.csdn.net/smooth00/article/details/81355110)
[jmeter多接口关联](https://blog.csdn.net/yh_ginny/article/details/85232859)
[正则表达式提取器讲解](https://blog.csdn.net/darkmanno5/article/details/80428275)

## [JMeter WebSocket Samplers官方文档](https://bitbucket.org/pjtr/jmeter-websocket-samplers/src/master/README.md)
在这里还是推荐下官方文档，还有issue ，相对来说是比较友好的。


**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

