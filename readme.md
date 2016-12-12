


# 阿里云直播App server接口介绍和部署

首先，需要了解阿里云相关产品可以通过如下链接：
## 直播
1. [直播快速开始](https://help.aliyun.com/document_detail/29957.html?spm=5176.doc45215.6.546.CjFllk)
2. [阿里云连麦对接文档.pdf](阿里云连麦对接文档.pdf)
3. [开始混流](https://help.aliyun.com/document_detail/44405.html?spm=5176.doc27155.6.697.cgWmgn)
4. [结束混流](https://help.aliyun.com/document_detail/44406.html?spm=5176.doc44405.6.698.t06Bxa)

## 消息服务
1. IM用的是阿里云MNS服务 [文档](https://help.aliyun.com/document_detail/27414.html?spm=5176.doc27494.6.539.xhdQKj)
2. 客户端订阅 [文档](websocket.pdf)

#部署和配置

1. [部署](./deploy/deployment.md)
2. [配置](./config/config.md)

# 接口说明：

1. [用户管理](#users)
2. [直播管理](#live) 
3. [连麦管理](#videocall)
4. [阿里通知](#alinotify)
5. [MNS管理](#alimns)

## 用户管理 | users
[TOP](#top)

1. [登录 /login](./user/login.md)
2. [直播间观众列表 /im/room/users](./user/roomusers.md)

## 直播管理 | live
[TOP](#top)

1. [直播列表 live/list](./live/list.md)
2. 创建直播 live/create](./live/create.md)
3. [观看直播 live/play](./live/play.md)
4. [主播退出直播 live/leave](./live/close.md)
5. [直播评论 live/comment](./live/comment.md)
6. [直播点赞 live/live](./live/like.md)
7. [结束观看直播 live/audience/leave](./live/leave.md)

## 连麦管理 | videocall
[TOP](#top)

1. [邀请连麦 videolcall/invite](./videocall/invite.md)
2. [连麦反馈 videocall/feedback](./videocall/feedback.md)
3. [连麦关闭 videocall/close](./videocall/close.md)

## 阿里MNS管理 | alimns
[TOP](#top)

1. [获取web socket链接信息 mns/topic/websocket/info](./mns/websocket.md)

## 阿里通知 | alinotify
[TOP](#top)

1. [阿里通知 videocall/ali/notify](./alinotify/notify.md)

# 推送消息
1. [推送消息](./msg/msg.md)


