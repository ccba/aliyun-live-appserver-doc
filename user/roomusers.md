[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#users)

# 获取房间用户列表

## 请求方式 ##
```ruby
    POST "/im/room/users"
```
## 是否需要登录 ##
    是

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
roomId|int|Y|房间ID

## 注意事项 ##
   无

## 返回结果 Json ##
>1.成功获取
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
