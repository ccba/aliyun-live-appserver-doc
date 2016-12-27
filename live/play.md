[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#live)

# 观看直播

## 请求方式 ##
```ruby
    POST "/live/play"
```

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
roomId|int|Y| 直播间ID
uid|string|Y| 用户ID


## 返回结果 Json ##

```python
{
  "code": 200,
  "message": "成功",
  "data": {
    "uid": "2",
    "name": "test5",
    "roomId": 230178951253721540,
    "playUrl": "http://videocall.play.danqoo.com/DemoApp/230178951253721540.flv",
    "mns":{
      "topic":'474c7658805b798814',
      "topicLocation": "http://125277.mns.cn-hangzhou.aliyuncs.com/topics/229820386403942828",
      "roomTag": "474c7658805b798814",
      "userRoomTag": "474c7658805b798814_2" #当前观众过滤消息的tag
    }
  }
}
```
