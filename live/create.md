[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#live)

# 创建直播

## 请求方式 ##
```ruby
    POST "/live/create"
```

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
uid|string|Y|用户ID
desc|string|N|描述


## 返回结果 Json ##

```python
{
  "code": 200,
  "message": "成功",
  "data": {
    "uid": 1,
    "name": "你好",
    "roomId": "474c7658805b798814",
    "rtmpUrl": "rtmp://videocall.push.danqoo.com/DemoApp/474c7658805b798814?auth_key=1475044685-0-0-3bef3969e641856d785dbeeb23f188a9",
    "playUrl": "http://videocall.play.danqoo.com/DemoApp/474c7658805b798814_mix.flv",
    "m3u8PlayUrl": "http://videocall.play.danqoo.com/DemoApp/474c7658805b798814_mix.m3u8",
    "rtmpPlayUrl": "rtmp://videocall.play.danqoo.com/DemoApp/474c7658805b798814_mix",
    "status": 1  ＃0:创建还未推流  1:在推流，2: 直播结束，  10: 连麦时系统创建的直播（主要是观众连麦时） 
    "type": 2, ＃1:观众  2:主播
    "isMixReady": false,
    "isMixed": false,
    "mns":{
      "topic":'474c7658805b798814',
      "topicLocation": "http://125277.mns.cn-hangzhou.aliyuncs.com/topics/229820386403942828",
      "roomTag": "474c7658805b798814",
      "userRoomTag": "474c7658805b798814_1"  #用于客户端过滤订阅消息给主播
    },
    "description": "test"
  }
}
```
