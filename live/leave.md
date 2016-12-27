[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#live)

# 观众离开直播

## 请求方式 ##
```ruby
    POST "/live/audience/leave"
```

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
roomId|int|Y|直播间ID
uid|int|Y|用户ID


## 返回结果 Json ##

```python
{
  "code": 200,
  "message": "成功"
}
}
```
