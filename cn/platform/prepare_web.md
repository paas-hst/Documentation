# 准备工作
在创建并初始化 HstRtcEngine 对象前，请确保你已完成环境准备、安装包获取等步骤。

## 初始化
Token用来进行登录认证，为保证账号的安全性，Token应该在开发者服务器端生成，

[点此下载](http://paas.hst.com/developer/downloadToken)Token生成代码

```
  let webRtcEngine = new HstRtcEngine()
  let appId = "you app id" // 系统为应用分配的 APP ID
  let token = "you token"  // token
  webRtcEngine.init(appId, token)
```

## 加入组
指定Group ID和User ID加入分组，Group ID和User ID由开发者定义。开发者要保证在同一分组中User ID不会冲突，同一分组下相同的User ID，后加入的会被拒绝掉。

```
  webRtcEngine.joinGroup(groupId, userId).then(() => {
      console.log('加入组成功')
  })
```

## 组成员通知
当远程人员推流时，在SDK里会触发onPublisher事件， 通过订阅这个事件，能够得到频道里已经推流的人员:

```
// 远程发布流事件
webRtcEngine.on('onPublisher', function (publisher) {
      //远程发布者ID
       console.log(publisher.userId); 
       //远程发布者 媒体id
       console.log(publisher.mediaId); 
       // 远程发布者的流类型 1：音频 2：视频
       console.log(publisher.mediaType);
})
```

相对应的也有onUnPublisher事件，当远程用户结束推流时，会触发这个事件：

```
webRtcEngine.on('onUnPublisher', function (publisher) {
  //远程发布者ID，在订阅方法时，要用到这个ID 
  console.log(publisher.userId); 
})
```

## 订阅onPublisher事件
当远程人员推流时，在SDK里会触发onPublisher事件， 通过订阅这个事件，能够得到频道里已经推流的人员:

```
// 远程发布流事件
webRtcEngine.on('onPublisher', function (publisher) {
      //远程发布者ID
       console.log(publisher.userId); 
       //远程发布者 媒体id
       console.log(publisher.mediaId); 
       // 远程发布者的流类型 1：音频 2：视频
       console.log(publisher.mediaType);
})
```

相对应的也有onUnPublisher事件，当远程用户结束推流时，会触发这个事件：

```
webRtcEngine.on('onUnPublisher', function (publisher) {
  //远程发布者ID，在订阅方法时，要用到这个ID 
  console.log(publisher.userId); 
})
```