[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#videocall)

# 邀请连麦

## 请求方式 ##
```ruby
    POST "/videocall/invite"
```
## 是否需要登录 ##
    是

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
inviterUid|string|Y|邀请连麦ID
inviteeUid |string|Y|被邀请连麦ID
liveRoomId |string|Y|直播间ID
type|string|N|混流类型 icture_in_picture 画中画  side_by_side 左右两边
inviterType|int|Y|邀请人是否为观众 #1是观众 2 主播

## 注意事项 ##
   无

## 返回结果 Json ##
>1.成功获取
```python
{
  "code": 200,
  "message": "成功"
}
```
