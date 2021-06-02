---
layout: post
title:  Websocket基础知识简记
category: 接口测试,理论知识
tags: [websocket接口测试]
---

# 特点：
* 低延时，数据格式轻量，性能开销小
* 服务器可以向客户端主动推送消息
* 基于TCP协议的应用层协议
* 默认端口 80（ws） 443(wss)
* 没有同源限制，客户端可以和任意服务器通信
* 标识符：ws/wss


# 原理
依赖HTTP协议进行第一次握手

**发送数据**
使用帧的形式发送。比如一条消息会分为几个frame,按照先后顺序传输出去。
优点： 大数据传输可以分片传输，不需要考虑数据大小导致的标志位不足够的情况
客户端发送的数据帧需要经过掩码处理。服务端发送的数据不能经过掩码处理。
帧： 帧类型标识码，负载长度，负载（扩展内容和应用内容）
帧类型：4位长的Opcode的值表示。
* Opcode==0 继续
* Opcode==1 文本帧
* Opcode==2 二进制帧
* Opcode==3-7 未来使用（非控制帧）
* Opcode==8 关闭连接
* Opcode==9 ping
乙方收到ping ,应当立即发送pong作为响应。
* Opcode==10 pong
* Opcode==11-15 未来使用（控制帧）

# Header
Sec-WebSocket-Key : Base64 encode ,浏览器随机生成，用于验证服务器是否是websocket助理
Sec-WebSocket-Version : 告诉服务器所使用的websocket draft 协议版本

response:
Sec-WebSocket-Accept: 经过服务器确认并且加密过后的Sec-WebSocket-Key

# 心跳重连机制
新名词，这又是什么鬼？
出现断开但是没有触发onclose事件
* 简单了解下websocket连接实现原理
后端：
建立连接 - onopen - onmessage(收到客户端消息后调用的方法) - sendmessage(发送消息给客户端)-onclose
异常情况：onerror: 发生错误时调用
前端：
建立连接 - onoopen - onmessage(收到服务端消息后调用的方法) -onclose(客户端主动断开连接或发生异常时断开连接)
异常情况：onerror: 发生错误时调用

网上简单看了一下，实现代码基本上是js.看不太懂。大概理解就是，定时向服务器发送信息（类似发送ping），看看服务器有没有返回pong,没有的话就重连。


# 问题
1. websocket和socket的区别
在我理解，其实，他们之间没什么关系，完全是两个东西。
socket 要了解的话，需要了解下《计算机网络》相关只是。
2. 全双工是什么？
允许服务器和客户端同时发送消息
3. 断掉连接后怎么办？？？？
很多websocket库都有自带ping，pong


# 参考
[微信,QQ 这类 IM app 怎么做——谈谈 Websocket](https://halfrost.com/ios_weixin_qq_websocket/)
[websocket教程-阮一峰](http://www.ruanyifeng.com/blog/2017/05/websocket.html)
[websocket和socket的区别](https://www.jianshu.com/p/59b5594ffbb0/)
[WebSocket的心跳重连机制](https://blog.csdn.net/qq_33922980/article/details/102646295)

**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
