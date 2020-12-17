# 准备工作

在调用Web SDK接口之前，需要做一些准备工作。

## 开发环境

请确保满足以下开发环境要求:

- 音视频通信，建议使用Chrome 70+浏览器
 
- 屏幕共享，需要使用Chrome 72+浏览器

- 非本机测试（localhost）必须使用https协议

## 创建应用

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。

2. 配置使用相关产品并上线应用。

3. 获取 **App ID** 和 **App Secret**。

## 获取 Token

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


## 添加 SDK

1. 下载 [Web SDK](http://paas.hst.com/developer/downloadSDK)。
 
2. 将解压后的JS文件放到到项目路径下。

3. 在项目种引用SDK。