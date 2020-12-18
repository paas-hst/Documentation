
# 准备工作

在进行微信小程序开发之前，需要做一些准备工作。

## 开发环境

- 安装微信开发者工具。
- 微信基础库版本2.9.0以上。

## 创建应用

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。

2. 配置使用相关产品并上线应用。

3. 获取 **App ID** 和 **App Secret**。

## 获取Token

安全起见，生产环境，Token应该在业务服务器上生成，客户端需要登录鉴权后才能获取Token，[点击此处](http://customer.paas.hst.com/code) 获取Token生成代码。  

为了方便测试，我们提供了一个在线生成临时Token的RESTFUL接口，建议使用POSTMAN工具。 

接口访问方式如下：

| 参数 | 值 |
| :-: | :- |
| Method | POST |
| URL | https://paas-token-gen.haoshitong.com/generate/token |
| Header | Content-type: application/json |
| Body | { "appId": "7a02a8217cd541f990152ea666ee24bf","appSecret": "42de63b19db7fda7"} |
| Response | {"code": 0, "message": "OK","result": "here is the token"} |

> 建议上线后创建新的应用，使用新的App ID和Token。

推荐使用POSTMAN工具获取临时Token，如下图所示：

<img alt="postman.png" src="http://fs.hst.com/download/paas/images/documentation/postman.png" align="center" />


> 注意Body的内容格式选择“raw”，检查appId和appSecret前后是否包含额外的空格。


## 添加SDK

1. 下载 [WeChat SDK](http://paas.hst.com/developer/downloadSDK)。
 
2. 将解压后的JS文件放到到项目路径下。

3. 在项目种引用SDK。

## 添加组件

微信小程序的音视频互动都是通过live-pusher和live-player组件来实现的，但是直接使用这两个组件，处理起来比较繁杂，因此，腾讯提供了一个webrtc-room的组件，内部封装live-pusher和live-player组件调用，对外提供了加入房间、广播音视频等易用接口，大大提升了上层应用的开发效率。

如无特殊要求，强烈建议在项目使用webrtc-room组件进行开发，[点此](https://github.com/TencentVideoCloudMLVBDev/MiniProgram/tree/master/wxlite/pages/components/webrtc-room)获取webrtc-room最新代码，你可以直接使用此组件，也可对组件进行定制修改。

当然，也可以使用DEMO中的webrtc-room组件，DEMO中对组件进行了定制化修改，可根据需要进行选择。

## 初始化

创建引擎对象，调用init方法进行初始化。

```js
let hstRtcEngine = new HstRtcEngine();
hstRtcEngine.init().then(() => {
    console.log("Init success.");
}).catch(() => {
    console.log("Init failed!");
})
```

## 登录平台

调用login接口登录云通信平台。

```js
let options = {
    appId: '7a02a8217cd541f990152ea666ee24bf',
    token: 'xxxxxxxxxx',
    companyId: "",
    userId: 'user1',
	mutextType: 'Web', 
    forceLogin: false,
	accessUrl: null,
    extendInfo: ''
};

hstRtcEngine.login(options).then(() => {
    console.log("Login success.");
}).catch(() => {
    console.log("Login failed!");
})
```

## 加入分组

调用joinGroup加入分组，接口返回“sdkAppId”、“serverUserId”、“userSig”，“serverRoomId”“privateMapKey”，将这些变量设置到webrtc-room组件的相关属性，可加入腾讯房间。

```js
hstRtcEngine.joinGroup(groupId).then(() => {
    console.log("Join group success.");
}).catch(() => {
    console.log("join group failed!");
})
```