# 集成客户端
本文将介绍如何集成Web SDK，需要准备的开发环境，包含前提条件及 SDK 集成方法等内容。

## 前提条件

请确保满足以下开发环境要求:

- 音视频通信，建议使用Chrome 70+浏览器
- 屏幕共享，需要使用Chrome 72+浏览器
- Web App非本机测试必须使用https协议

## 创建项目并获取 App ID

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。
2. 配置使用相关产品并上线应用。
3. 点击 **应用** 下的 **应用列表** ，在详情页面获取到 **App ID**。

## 获取 Token

安全起见，生产环境，Token应该在业务服务器上生成，客户端需要登录鉴权后才能获取Token。  
为了方便测试，我们提供了一个在线生成token的RESTFUL接口，用来临时生成token，上线后建议更换App ID。 

接口访问方式如下：

| :-: | :- |
| Method | POST |
| URL | https://paas-token-gen.haoshitong.com/generate/token |
| Header | Content-type: application/json |
| Body | { "appId": "7a02a8217cd541f990152ea666ee24bf","appSecret": "42de63b19db7fda7"} |
| Response | {"code": 0, "message": "OK","result": "here is the token"} |


## 添加 SDK
1. 下载 [Web SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。 
2. 将JS文件保存到你所操作的项目下。
3. 在项目相应的前端页面文件中，对JS文件进行引用。

## 相关文档
完成了客户端集成后，你可以使用 SDK，使用各个产品的功能：

- [准备工作](../prepare_web.md)