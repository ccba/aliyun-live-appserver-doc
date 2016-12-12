# 登录

## 请求
```ruby
   POST /login
```

## 入参
名称|类型|必选|说明
---|:---|:---|:---
name|string|Y|
password|string|N|

## 返回
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
