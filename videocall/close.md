# 连麦结束关闭

## 请求方式 ##
```ruby
    POST "/videocall/close"
```
## 是否需要登录 ##
    是

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
closeRooomId|int|Y|关闭连麦房间ID
notifiedRoomId |int|Y|被通知连麦关闭房间ID

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
