# 使用Salt REST

## Salt HTTP类库
* Salt HTTP支持3个类库：tornado（默认）、requests和urllib2，可以在Master配置中设置backend参数

### 使用http.query方法
```
没有返回内容举例：
# salt myminion http.query https://www.google.com/
# salt-run http.query https://www.google.com/
有返回内容举例：
# salt-run http.query https://www.google.com/ text=True status=True headers=True
则结果返回一个字典，包含HTTP状态码（status code）、header以及body的内容
```
* GET与POST
```
# salt-run http.query http://mydomain.com/?user=larry
# salt-run http.query http://mydomain.com/ POST data='{}'
```
* Salt HTTP客户端能够自动解码接收到的返回数据，若将decode参数设置为True，Salt会自动尝试侦测返回的数据是XML还是JSON，除非明确指定decode_type
```
# salt-run http.query https://api.github.com/ decode=True decode_type=json
另：当decode为True时，返回的数据会在dict字段中，而不是text为True时的text字段
```

### 使用http.query State
* 在反应器中使用http.query，每次State完成后，都会发送一个包含结果的事件给Master

## 理解Salt API
* Salt API是基于Salt封装的REST接口，目前Salt API支持3个Web模块：CherryPy、Tornado和WSGI

### 创建SSL证书
* 通过openssl等命令获取

### 使用webhook
* webhook用于通过HTTP/HTTPS的一次性调用来处理命令，不需要先获取token


[返回目录](../CONTENTS.md)