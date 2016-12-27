[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#alimns)

# 获取websocket的连接信息

## 请求方式 ##
```ruby
    POST "/mns/topic/websocket/info"
```

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
topic|string|Y|主题
subscriptionName|string|N|订阅名字 默认和topic名字一样


## 返回结果 Json ##

```python
{
  "code": 200,
  "message": "成功",
  "data": {
    "authentication": "Fa91Q+YDqsa7CQOMHyYXE7OFw=",
    "topicWebsocketServerIp": "10.152.251.77",
    "accountId": "12277",
    "accessId": "Q1dfW3pJSOJf6"
  }
}
```
