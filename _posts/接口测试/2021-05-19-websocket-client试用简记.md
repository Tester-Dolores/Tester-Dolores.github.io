---
layout: post
title:  websocket-client 试用简记
categories: 接口测试 Python
tags: [websocket接口测试,Python库]
---

# 尝试重写WebSocketApp
按照个人理解，某些处理是共用的，因此定义ws默认的on_error,on_close,on_ping,on_pong
就目前使用on_message,on_open所作的处理可能会有不同。
```
class MyWebsocket(websocket.WebSocketApp):
	url="ws://" # websocket url
	def on_error(mw, error):
	    print(error)
	    print("！！！！！！！！！发生未知错误！！！！！！！！！\n关闭连接........\n")
	    mw.close()

	def on_close(mw):
		print("===== closed =======\n")

	def on_ping(mw,message):
	    print("Got a Ping:")
	    print(message)

	def on_pong(mw,message):
	    print("Got a Pong:")
	    print(message)

	def on_data(ws,message,datatype,continueflag):
		print ("D >>> "+str(len(message))+" "+message)

	def __init__(self,url=url,on_error=on_error,on_close=on_close,on_pong=on_pong,on_ping=on_ping, header=None,
		on_open=None, on_message=None,
		on_cont_message=None,
		keep_running=True, get_mask_key=None, cookie=None,
  		subprotocols=None,
		on_data=on_data,is_connect=0,is_sendwav=0,user_id = ""):
		websocket.WebSocketApp.__init__(self, url,on_error=on_error,on_close=on_close,on_pong=on_pong,on_ping=on_ping, header=None,
		on_open=None, on_message=None,
		on_cont_message=None,
		keep_running=True, get_mask_key=None, cookie=None,
  		subprotocols=None,
		on_data=on_data)
		self.on_message=on_message
		self.on_open=on_open
		self.is_connect = is_connect
		self.is_sendwav = is_sendwav
		self.user_id = user_id

```
试用：
```
mywebsocket = MyWebsocket(on_open=on_open,on_message=on_message)
mywebsocket.run_forever(ping_interval=60,ping_timeout=30)
```
# Option
## 设置超时连接
`websocket.setdefaulttimeout(5)`
## enabletrace
`websocket.enableTrace(True)`

# 发送文本和binary
## json格式
```
def send_json(ws,data,operateName="test"):
	print("\n【"+operateName+"】")
	ws.send(json.dumps(data))
	pprint(data)
	set_waiting()
```
试用：
```
data={
			"user_id":"123",
			"user_name": "dolores"
		}
send_json(mywebsocket,data)
```

## wav
```
def sendWAV(wav):
		print("============开始发送音频数据==================")
		step = 3200
		with open(wav, 'rb') as f:
			while True:
				read_data = f.read(step)
				if read_data:
					self.mywebsocket.send(read_data, ABNF.OPCODE_BINARY)
				if len(read_data) < step:
					break
				set_waiting(0.1)
		print("============结束发送音频数据================")
		set_waiting(10)

sendWAV("./test.wav")
```
==================2021-05-20 修改 ========================
阴差阳错之下发现了python 自带的wave库.....
```
import wave
def sendWAV(self,wav):
		print("============开始发送音频数据==================")
		step = 1600 
		with wave.open(wav, 'rb') as f:
			while True:
				read_data = f.readframes(step)
				if read_data:
					self.mywebsocket.send(read_data, ABNF.OPCODE_BINARY)
				if len(read_data) < step:
					break
				set_waiting(0.1)
		print("============结束发送音频数据================")
		set_waiting(15)
```
# 接收服务器消息
## on_message
```
def on_message(ws, message):
	print("【server message】\n"+message)
  # 服务端返回的是字符串，可按需转成json格式
	message = json.loads(message)
  print(message["id"])
```
## on_data
```
def on_data(ws,message,datatype,continueflag):
  print ("D >>> "+str(len(message))+" "+message)
```

**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**

**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
