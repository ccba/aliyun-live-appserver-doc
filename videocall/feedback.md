[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#videocall)

# 连麦反馈(是否同意连麦)

## 请求方式 ##
```ruby
    POST "/videocall/feedback"
```
## 是否需要登录 ##
    是

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
inviterUid|string|Y|邀请连麦ID
inviteeUid |string|Y|被邀请连麦ID
status|int|Y|是否同意状态 #1同意 2 不同意
type|string|N|混流类型 picture_in_picture 画中画  side_by_side 左右两边
inviterType|int|Y|邀请是否为观众 #1是观众 2 主播
inviteeType|int|Y|被邀请是否为观众 #1是观众 2 主播


## 注意事项 ##
   无

## 返回结果 Json ##
>1.成功获取
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
