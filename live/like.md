[**返回**](https://github.com/ccba/aliyun-live-appserver-doc#live)

# 直播点赞

## 请求方式 ##
```ruby
    POST "/live/like"
```

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
uid|string|Y|用户ID
roomId|int|Y|直播间ID

## 返回结果 Json ##

```python
{
  "code": 200,
  "message": "成功"
}
```
