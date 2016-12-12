# 直播评论

## 请求方式 ##
```ruby
    POST "/live/comment"
```
## 是否需要登录 ##
    是

## 请求参数 ##

参数名|数据类型|必选|说明
:------:|:------:|:------:|:------
uid|string|Y|用户ID
roomId|int|Y|直播间ID
comment|string|Y|评论内容

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
