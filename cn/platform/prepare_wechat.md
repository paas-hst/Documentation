
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

微信小程序的音视频互动都是通过live-pusher和live-player组件来实现的，但是直接使用这两个组件，处理起来比较繁杂，因此，腾讯提供了一个webrtc-room的组件，内部封装live-pusher和live-player组件调用，对外提供了加入房间、广播音视频等易用接口，大大方便了上层应用开发。

如无特殊要求，建议使用webrtc-room组件进行开发，[点此](https://github.com/TencentVideoCloudMLVBDev/MiniProgram/tree/master/wxlite/pages/components/webrtc-room)获取最新代码，可以直接使用此组件，也可以在此基础上进行修改，当然，也可以使用DEMO中的webrtc-room组件，DEMO中进行了定制化修改，可根据需要进行选择。

