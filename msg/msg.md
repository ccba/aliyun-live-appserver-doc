[**返回**](https://github.com/ccba/aliyun-live-appserver-doc)

#### 邀请连麦推送 ####
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

#### 同意连麦推送 ####
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

#### 不同意连麦推送 ####
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

#### 结束连麦推送（混流不一定结束） ####
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


#### 连麦混流成功推送 ####
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

#### 评论推送 ####
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

#### 点赞推送 ####
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

#### 直播结束推送 ####
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

#### 开始推流推送####
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

#### 中断推流推送####
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

#### 混流失败推送####
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

#### 连麦混流结束成功推送####
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

#### 连麦过程中的启动结束混流命令状态推送####

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
#### 混流可用通知 ####
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
