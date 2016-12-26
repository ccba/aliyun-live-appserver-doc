


# 阿里云直播App server部署和接口介绍 node版

首先，需要了解阿里云相关产品可以通过如下链接：
## 直播
1. [直播快速开始](https://help.aliyun.com/document_detail/29957.html?spm=5176.doc45215.6.546.CjFllk)
2. [阿里云连麦对接文档.pdf](./pdf/阿里云连麦对接文档.pdf)
3. [开始混流](https://help.aliyun.com/document_detail/44405.html?spm=5176.doc27155.6.697.cgWmgn)
4. [结束混流](https://help.aliyun.com/document_detail/44406.html?spm=5176.doc44405.6.698.t06Bxa)
5. [连麦地址效果说明](./address.md)
6. [App server连麦基本流程](./pdf/连麦AppServer处理流程图.pdf)

## 消息服务
1. 阿里云MNS服务 [文档](https://help.aliyun.com/document_detail/27414.html?spm=5176.doc27494.6.539.xhdQKj)
2. 客户端订阅 [文档](./pdf/websocket.pdf)

# 代码和配置

## 源码

[appserver源码](https://github.com/ccba/aliyun-live-appserver-code)

## 配置

    配置是在config.js文件里

        ```ruby
        config = {
          port: 4000, //服务端口号
          ip: "localhost", //服务IP地址
          redis: {
            password: "videocall", //redis连接密码
            host: 'localhost', //redis的host
            port: 6379, //redis端口号
            keyprefix: 'mns'
          },
          ali: {
            mnsTopic: {  //阿里云mns服务信息配置
              topicWebsocketServerIp: "115.28.250.251",
              subscriptionEndpoint: "WebSocket"
            },
            ownerId: '1252745454',
            accessKeyID: 'Q1dfW3pBESJS',
            accessKeySecret: 'sdDpBtlS9Bcg80eU5cwTMzvGU',
            mnsVersion: '2015-06-06', //mns接口版本
            region: 'cn-qingdao-internal-japan-test', 
            // region: 'cn-hangzhou',
            commonParams: {
              Format: 'json',
              SignatureMethod: 'HMAC-SHA1',
              SignatureVersion: '1.0'
            },
            urls: {
              cdn: { //cdn地址和版本
                url: 'https://cdn.aliyuncs.com',
                version: '2014-11-11'
              }
            }
          },
          videocall: {
            templateName: '_mix' //CDN混流模版名称，默认为mix
          },
          //用于生产直播推流和播放地址 这个要到阿里云控制台配置自己的推流和播放域名
          appName: 'DemoApp',
          authKey: 'qupaivid', //用于生产推流鉴权的key， 如果为空将不添加auth_key参数
          appName: 'DemoApp',
          isCenterPush: false, //是否中心推流 rtmp://video-center.alivecdn.com/DemoApp/3ff0274890?vhost=videocall.play.aliyun.com
          rtmpHost: 'videocall.push.aliyun.com', //推流host域名
          playHost: 'videocall.play.aliyun.com', //播放host域名
        }
        ```


## 依赖环境

### 手动安装

#### Node.js
参考官网：https://nodejs.org/en/download/   安装完后，在命令窗口输入：node -v  验证是否安装成功
#### Redis
官网下载安装redis, 启动服务，参考:http://www.runoob.com/redis/redis-install.html

### 镜像市场安装
在申请阿里云ECS时， 镜像类型选择**镜像市场**, 从镜像市场选择，输入关键字**Nodejs集成环境**过滤,选择对应操作系统的镜像。

## 安装Appserver依赖

获取代码，进入aliyun-live-appserver-code目录 运行命令:
```python
cnpm install
```
## 运行程序
进入aliyun-live-appserver-code目录， 运行命令：
```python
node app.js
```
## 特殊情况处理
因为连麦异常通知消息包含空格， 导致appserver消息接受不到,CDN的要下次发布时候添加decode，临时解决方案是这个回调通过nginx代理跳转， 下一版本就不用这一步了。

### 安装nginx
1. 安装参考：http://blog.csdn.net/molingduzun123/article/details/51850925  zlib可以不安装
2. 配置ngix.conf, 添加端口

```python
   server {
        listen 9020;
        server_name localhost;
        index index.html;

        location /ali/mix/status/notify  {
            set $args MainMixDomain=$arg_MainMixDomain&MainMixApp=$arg_MainMixApp&MainMixStream=$arg_MainMixStream&MixDomain=$arg_MixDomain&MixApp=$arg_MixApp&MixStream=$arg_MixStream=$arg_MixStream&MixType=$arg_MixType&MixTemplate=$arg_MixTemplate&Event=MixResult&Code=$arg_Code&Message=$arg_Code;

            proxy_pass http://localhost:4000/ali/mix/status/notify;
          }
        } 
```

## 使用PM2管理程序（可选择）

### 安装进程管理器pm2
运行命令：cnpm install pm2 -g

### 启动程序
进入aliyunlivedemo目录， 运行: npm run prod

### 关闭程序
 进入aliyunlivedemo目录， 运行: npm run stop

# 接口说明

## 用户管理

### [登录 /login](./user/login.md)

#### 请求
    ```ruby
       POST /login
    ```

#### 入参
    名称|类型|必选|说明
    ---|:---|:---|:---
    name|string|Y|
    password|string|N|

#### 返回
    ```json
    {
      "code": 200,
      "message": "成功",
      "data": {
        "id": "1",
        "name": "est"
        }
      }
    }
    ```

### [直播间观众列表 /im/room/users](./user/roomusers.md)

#### 请求方式 ##
```ruby
    POST "/im/room/users"
```

#### 请求参数 ##

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    roomId|int|Y|房间ID

#### 返回结果 Json ##

    ```python
    {
      "code": 200,
      "message": "成功",
      "data": [
        {
          "name": "ccv",
          "id": "1"
        },
        {
          "name": "ddf",
          "id": "2"
        }
      ]
    }
    ```


## 直播管理

### [直播列表 live/list](./live/list.md)

#### 请求方式
    ```ruby
      GET {baseUrl}/live/list
    ```

#### 请求参数

    名称|类型|必选|含义
    :---|:---|:---|:---
    roomId|int|N|直播间ID

#### 返回
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

### [创建直播 live/create](./live/create.md)

#### 请求方式 
    ```ruby
        POST "/live/create"
    ```

#### 请求参数 

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    uid|string|Y|用户ID
    desc|string|N|描述

#### 返回结果 Json 

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

### [观看直播 live/play](./live/play.md)

#### 请求方式 
    ```ruby
        POST "/live/play"
    ```

#### 请求参数 

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    roomId|int|Y| 直播间ID
    uid|string|Y| 用户ID

#### 返回结果 Json 

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

### [主播退出直播 live/leave](./live/close.md)

#### 请求方式 
    ```ruby
        POST "/live/leave"
    ```

#### 请求参数

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    roomId|int|Y|直播间ID

#### 返回结果 Json

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    }
    ```

### [直播评论 live/comment](./live/comment.md)

#### 请求方式 
    ```ruby
        POST "/live/comment"
    ```

#### 请求参数 

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    uid|string|Y|用户ID
    roomId|int|Y|直播间ID
    comment|string|Y|评论内容

#### 返回结果 Json 

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    ```

### [直播点赞 live/live](./live/like.md)

#### 请求方式 
    ```ruby
        POST "/live/like"
    ```

#### 请求参数 

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    uid|string|Y|用户ID
    roomId|int|Y|直播间ID

#### 返回结果 Json 

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    ```


### [结束观看直播 live/audience/leave](./live/leave.md)

#### 请求方式 
    ```ruby
        POST "/live/audience/leave"
    ```

#### 请求参数 

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    roomId|int|Y|直播间ID
    uid|int|Y|用户ID

#### 返回结果 Json 

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    }
    ```

## 连麦管理 

### [邀请连麦 videolcall/invite](./videocall/invite.md)

#### 请求方式 
    ```ruby
        POST "/videocall/invite"
    ```

#### 请求参数

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    inviterUid|string|Y|邀请连麦ID
    inviteeUid |string|Y|被邀请连麦ID
    liveRoomId |string|Y|直播间ID
    type|string|N|混流类型 icture_in_picture 画中画  side_by_side 左右两边
    inviterType|int|Y|邀请人是否为观众 #1是观众 2 主播


#### 返回结果 Json

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    ```


### [连麦反馈 videocall/feedback](./videocall/feedback.md)

#### 请求方式 
    ```ruby
        POST "/videocall/feedback"
    ```

#### 请求参数

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    inviterUid|string|Y|邀请连麦ID
    inviteeUid |string|Y|被邀请连麦ID
    status|int|Y|是否同意状态 #1同意 2 不同意
    type|string|N|混流类型 picture_in_picture 画中画  side_by_side 左右两边
    inviterType|int|Y|邀请是否为观众 #1是观众 2 主播
    inviteeType|int|Y|被邀请是否为观众 #1是观众 2 主播


#### 返回结果 Json

    ```python
    {
      code:200,
      message: “”
      data:{   
             ＃同意连麦时返回如下值
             ＃副麦（被邀麦方）短延时播放地址和主麦（邀麦方）推送地址通过消息发送给邀麦方
             inviterPlayUrl:””,  #主麦（邀麦方）短延时播放地址
             inviterRoomId:"244646650876789164"
             rtmpUrl: “”, #副麦（被邀麦方）推送地址
          }
    }

    ```

### [连麦关闭 videocall/close](./videocall/close.md)

#### 请求方式
    ```ruby
        POST "/videocall/close"
    ```

#### 请求参数

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    closeRooomId|int|Y|关闭连麦房间ID
    notifiedRoomId |int|Y|被通知连麦关闭房间ID


#### 返回结果 Json

    ```python
    {
      "code": 200,
      "message": "成功"
    }
    ```

## 阿里MNS管理

### [获取web socket链接信息 mns/topic/websocket/info](./mns/websocket.md)

#### 请求方式
    ```ruby
        POST "/mns/topic/websocket/info"
    ```

#### 请求参数

    参数名|数据类型|必选|说明
    :------:|:------:|:------:|:------
    topic|string|Y|主题
    subscriptionName|string|N|订阅名字 默认和topic名字一样

#### 返回结果 Json

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


## 阿里通知

### [阿里通知](./alinotify/notify.md)

#### 原始流推流／断流通知回调地址，[设置URL](https://help.aliyun.com/document_detail/35030.html)
    ```ruby
         "/ali/stream/notify"
    ```

#### 混流可用通知回调地址，参数请参考[阿里云连麦对接文档.pdf](./pdf/阿里云连麦对接文档.pdf)

    用于通知使用方是否可以以某路流为主流调用调用混流， 用户提用回调的URL。
    ```ruby
         "/ali/mix/status/notify"
    ```

#### 混流结果通知回调地址，参数请参考[阿里云连麦对接文档.pdf](./pdf/阿里云连麦对接文档.pdf)

    用于通知使用方混流的内容是否发生改变， 用户提用回调的URL。
    ```ruby
        "／ali/mix/availability/notify"
    ```


# 推送消息
## [推送消息](./msg/msg.md)

### 邀请连麦推送
    权重：4
    ```ruby
    {
      "data": {
          inviterUid: "12",
          inviterName:"名字" ,
          type:"side_by_side", #picture_in_picture 画中画  side_by_side 左右两
          inviterType:1  #邀请是否为观众 #1是观众 2 主播
      },
      type:1,
      time: 1367997715932
    }
    ```    

### 同意连麦推送
    权重：4
    ```ruby
    {
      "data":{ 
          inviteeUid: "名字",
          inviteeName: "名字",
          inviteeRoomId: "12",
          inviterRoomId: "13",
          inviteePlayUrl: "副麦短延时播放地址",
          rtmpUrl: "主麦推送地址",
          type: "side_by_side",
          status: 1
      },
      type:2,
      time: 1367997715932
    }
    ```

### 不同意连麦推送 
    权重：4
    ```ruby
    {
      data:{
          inviteeUid: 12,
          inviteeName:"name"
          status: 2  #1 同意 2 拒绝
      },
      type:3,
      time: 1367997715932
    }
    ```

### 结束连麦推送（混流不一定结束）
    权重：5
    ```ruby
    {
      data:{
          roomId: 12,
          uid: 12,
          name: "测试",
          notifiedRoomId: 13,
          notifiedUid: 14,
          notifiedName: "测试1"
      },
      type:4,
      time: 1367997715932
    }
    ```


### 连麦混流成功推送
    权重：5
    ```ruby
     {
      data:{
          inviterRoomid: 12,
          inviteeRoomid:13,
          inviterUid: 1,
          inviterName: 'inviterName',
          inviteeUid: 2,
          inviteeName: 'inviteeName',
          inviterMixPlayUrls:  [
    'http://videocall.play.danqoo.com/DemoApp/243211683177169332_mix360',
    'http://videocall.play.danqoo.com/DemoApp/243211683177169332_mix480'
           ],
          inviteeMixPlayUrls: [
    'http://videocall.play.danqoo.com/DemoApp/243211683177169332_mix360',
    'http://videocall.play.danqoo.com/DemoApp/243211683177169332_mix480'
          ]
      },
      type:5,
      time: 1367997715932
    }

    ```

### 评论推送

    权重：8
    ```ruby
    {
      data:{
          uid: 12,
          name: “name”,
          comment: “comment”
      },
      type:6,
      time: 1367997715932
    }
    ```

### 点赞推送 

    权重：9
    ```ruby
     {
      data:{
          uid: 12,
          name: “name”,
      },
      type:7,
      time: 1367997715932
    }

    ```

### 直播结束推送
    权重：5
    ```ruby
    {
      data:{
          roomId: 12
      },
      type:8,
      time: 1367997715932
    }

    ```

### 开始推流推送
    权重：5
    ```ruby
     {
      data:{
          uid: 1,
          name: “2222” 
          roomId: 12
        },
      type:9,
      time: 1367997715932
    }

    ```

### 中断推流推送
    权重：5
    ```ruby
    {
      data:{
          uid: 1,
          name: “2222”  
          roomId: 12
        },
      type:10,
      time: 1367997715932
    }

    ```

### 混流失败推送
    权重：5
    ```ruby
    {
      data:{
          inviterRoomid: 12,
          inviteeRoomid:13,
          inviterUid: 1,
          inviterName: 'inviterName',
          inviteeUid: 2,
          inviteeName: 'inviteeName'
      },
      type:14,
      time: 1367997715932
    }

    ```

### 连麦混流结束成功推送
    权重：5
    ```ruby
    {
      data:{
          roomId: 12,
          uid: 40,
          name: "放入肉",
          notifiedRoomId: 13,
          notifiedUid: 14,
          notifiedName: "测试1"
      },
      type:15,
      time: 1367997715932
    }

    ```

### 连麦过程中的启动结束混流命令状态推送

    调用阿里混流接口或结束混流接口中间的状态消息推送的
    权重：5

    code说明及处理请参考：
    [阿里视频云连麦对接文档.pdf](http://192.168.10.203/qupai.videocall/server/uploads/26c90d5c30a2ba165beec048db95a92c/阿里视频云连麦对接文档.pdf)
    ```ruby
    {
      data:{
          mainMixRoomId, // 主流房间ID
          mixRoomId, //副流房间ID
          mixType, //混流类型（ stream 或者 channel）
          mixTemplate, //混流模板
          event, //EventMix EventMixStop  开始混流，结束混流
          message, //错误描述 为空时表示成功，
          code:200 //说明请参考 阿里视频云连麦对接文档.pdf
      },
      type:16,
      time: 1367997715932
    }
    ```
### 混流可用通知
    权重：5
    ```ruby
    {
      data:{
          roomId: 12,
          type:2  //1：观众 2: 主播
      },
      type:17,
      time: 1367997715932
    }

    ```
