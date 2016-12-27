[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#live)

# 获取直播列表


## 请求方式
```ruby
  GET {baseUrl}/live/list
```

## 请求参数
名称|类型|必选|含义
:---|:---|:---|:---
roomId|int|N|直播间ID

## 返回
```json
{
  "code": 200,
  "message": "成功",
  "data": [
    {
      "uid": "8070355f",
      "name": "qqqqqqqq",
      "roomId": "230176387716088260",
      "rtmpUrl": "rtmp://videocall.push.danqoo.com/DemoApp/230176387716088260?auth_key=1471243317-0-0-69544892580969bfbb3c86112c532d1b",
      "playUrl": "http://videocall.play.danqoo.com/DemoApp/230176387716088260.flv",
      "status": 1,
      "type": 2, ＃1:观众  2:主播
      "isMixReady": true, # true 编码流已经准备好
      "isMixed": false, ＃true 混流成功
      "mns":{
        "topic":'474c7658805b798814', #直播间topic，用于客户端订阅消息
        "topicLocation": "http://125277.mns.cn-hangzhou.aliyuncs.com/topics/229820386403942828",
        "roomTag": "474c7658805b798814" ＃直播间tag, 用于客户端过滤订阅消息
      },
      "description":"XX的直播"
    },
    {
      "uid": "e6fdb3ab",
      "name": "499455",
      "roomId": "229820386403942828",
      "rtmpUrl": "rtmp://videocall.push.danqoo.com/DemoApp/229820386403942828?auth_key=1471160429-0-0-6df7a7e4326d86a019e2160b9549956a",
      "playUrl": "http://videocall.play.danqoo.com/DemoApp/229820386403942828.flv",
      "status": 0,
      "type": 2, ＃1:观众  2:主播
      "isMixReady": true, # true 编码流已经准备好
      "isMixed": false, ＃true 混流成功
      "mns":{
        "topic":'474c7658805b798814',
        "topicLocation": "http://125277.mns.cn-hangzhou.aliyuncs.com/topics/229820386403942828",
        "roomTag": "474c7658805b798814"
      },
      "description":"XX的直播"
    }
  ]
}
```
