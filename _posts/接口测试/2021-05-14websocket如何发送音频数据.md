---
layout: post
title:  websocket 如何发送音频数据
category: 接口测试 
tags: [websocket接口测试]
---

# jmeter
1.java
AudioSystem.getAudioInputStream(File)

到底如何转换？？

java sound


2. beanshell 预处理
`vars.put("bytes", s);`

ws write
${bytes}

暂时失败告终，有空再学习.....


# python websocket-client
对jmeter 实在是不怎么熟悉，先用比较熟悉的python 实现一下吧。

## 短连接
```
import websocket
ws = websocket.WebSocket()
ws.connect(url)
ws.send("123")
print(ws.recv())
ws.close()
```

## 长连接
```
import websocket

def on_message(ws,message):
  print(message)

# 这里的ws必须和on_message的ws同名
ws = websocket.WebSocketApp(url,on_message=on_message)
ws.run_forever()
```

[个人试用简记](https://www.cnblogs.com/Tester_Dolores/p/14786502.html)

# js
https://github.com/websockets/ws
https://blog.csdn.net/qq_32252957/article/details/88586497

electron 打包成exe
https://github.com/electron/electron

**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
