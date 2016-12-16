[返回](https://github.com/ccba/aliyun-live-appserver-doc)
配置是在config.js文件里
```ruby
config = {
  port: 4000, //服务端口号
  ip: "localhost", //服务IP地址
  redis: {
    password: "videocall", //redis连接密码
    host: 'localhost', //redis的host
    port: 6379, //redis端口号
    keyprefix: 'mns'
  },
  ali: {
    mnsTopic: {  //阿里云mns服务信息配置
      topicWebsocketServerIp: "115.28.250.251",
      subscriptionEndpoint: "WebSocket"
    },
    ownerId: '1252745454',
    accessKeyID: 'Q1dfW3pBESJS',
    accessKeySecret: 'sdDpBtlS9Bcg80eU5cwTMzvGU',
    mnsVersion: '2015-06-06', //mns接口版本
    region: 'cn-qingdao-internal-japan-test', 
    // region: 'cn-hangzhou',
    commonParams: {
      Format: 'json',
      SignatureMethod: 'HMAC-SHA1',
      SignatureVersion: '1.0'
    },
    urls: {
      cdn: { //cdn地址和版本
        url: 'https://cdn.aliyuncs.com',
        version: '2014-11-11'
      }
    }
  },
  videocall: {
    templateName: '_mix' //CDN混流模版名称，默认为mix
  },
  //用于生产直播推流和播放地址 这个要到阿里云控制台配置自己的推流和播放域名
  appName: 'DemoApp',
  authKey: 'qupaivid', //用于生产推流鉴权的key， 如果为空将不添加auth_key参数
  appName: 'DemoApp',
  isCenterPush: false, //是否中心推流 rtmp://video-center.alivecdn.com/DemoApp/3ff0274890?vhost=videocall.play.aliyun.com
  rtmpHost: 'videocall.push.aliyun.com', //推流host域名
  playHost: 'videocall.play.aliyun.com', //播放host域名
}
```
