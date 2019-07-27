# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件

请确保满足以下开发环境要求:

- 安装Chrome 75+浏览器

- 确保部署环境为localhost或https协议

## 添加 SDK

1. 下载 [Web SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。 
2. 将JS文件保存到你所操作的项目下。
3. 在项目相应的前端页面文件中，对JS文件进行引用。


在创建并初始化 HstRtcEngine 对象前，请确保你已完成环境准备、安装包获取等步骤。

## 初始化

使用SDK之前必须初始化。Token用来进行登录认证，为保证账号的安全性，Token应该在开发者服务器端生成。其中，Token为字符串，用来校验身份和鉴权，由开发者自己生成，具体请参考“平台介绍->基本概念->应用鉴权”；User ID也是字符串，由开发者定义，用来唯一标识一个用户，开发者必须保证App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```js
  let webRtcEngine = new HstRtcEngine()
  let appId = "you app id" // 系统为应用分配的 APP ID
  let token = "you token"  // token
  webRtcEngine.init(appId, token)
```

## 加入分组

通过指定Group ID和User ID加入分组，Group ID和User ID由开发者定义。开发者要保证同一App下Group ID不会冲突，在同一分组中User ID不会冲突。


```js
  webRtcEngine.joinGroup(groupId, userId).then(() => {
      console.log('加入组成功')
  })
```

> 同一分组下相同的User ID，后加入的会被拒绝掉。

## 订阅事件

当远端广播音视频时，在SDK里会触发 onPublisher 事件。通过订阅这个事件，能够知道谁（User ID）广播了流；广播了什么类型（Media Type）的流：音频、视频；以及流的编号（Media ID）。

```js
// 远程发布流事件
webRtcEngine.on('onPublisher', function (publisher) {
       // 远程发布者ID，在订阅方法时，要用到这个ID
       console.log(publisher.userId); 
       // 远程发布者 媒体id
       console.log(publisher.mediaId); 
       // 远程发布者的流类型 1：音频 2：视频
       console.log(publisher.mediaType);
})
```

相对应的也有 onUnPublisher 事件，当远端停止广播时，会触发这个事件。

```js
webRtcEngine.on('onUnPublisher', function (publisher) {
  //远程发布者ID，在订阅方法时，要用到这个ID 
  console.log(publisher.userId); 
})
```

> 一个用户同一类型的流可能会有多个，比如接了多个摄像头。