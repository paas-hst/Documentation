# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 开发环境

请确保满足以下开发环境要求:

- 音视频通信，建议使用Chrome 70+浏览器
 
- 屏幕共享，需要使用Chrome 72+浏览器

- Web App非本机测试（localhost）必须使用https协议

## 创建项目并获取 App ID

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。

2. 配置使用相关产品并上线应用。

3. 点击 **应用** 下的 **应用列表** ，在详情页面获取到 **App ID** 和 **App Secret**。

## 获取 Token

安全起见，生产环境，Token应该在业务服务器上生成，客户端需要登录鉴权后才能获取Token，[点击此处](http://customer.paas.hst.com/code) 获取Token生成代码。  

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


## 初始化

创建HstRtcEngine对象，调用init方法进行初始化，如果是公有云测试，初始化参数为空；如果是私有云测试，此处填Access服务器地址。

```js
  let webRtcEngine = new HstRtcEngine();
  webRtcEngine.init(/*access url for private cloud*/)
  .then(() => {
    console.log("Init success.");
  })
  .catch(err => {
    console.log("Init failed!", err);
  })
```

## 登录

初始化完成后，立即登录平台。appId和token参数用来鉴权；companyId表示属于哪个企业组织，默认填空即可；userId由开发者定义，具体请参考“平台介绍->基本概念->User ID”。

```js
  let param = {
    appId: '7a02a8217cd541f990152ea666ee24bf',
    token: '001Sx04XAA406DvYyD8J3oEh/eSZFnogbLaFnwlXozD6QfHszwvHlCNRVj3wjIxldlRYRG28cGFdK9xgku3fhdMKY2pB3j1It4Omq8Quxx4xFH/2h3MbrWmsVCjh/N1cfsx',
    companyId: '',
    userId: 'test'
  };
  webRtcEngine.login(param)
  .then(() => {
    console.log("Login success.");
  })
  .catch(err => {
    console.log("Login failed!", err);
  })
```

## 加入分组

登录成功后，通过指定Group ID加入分组，Group ID由开发者定义，开发者要保证同一App下Group ID不会冲突。具体请参考“平台介绍->基本概念->Group ID”。

```js
  webRtcEngine.joinGroup(groupId)
  .then(() => {
    console.log("Join group success.");
  })
  .catch(err => {
    console.log("join group failed!", err);
  })
```

> User ID和Group ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，后登录的会被拒绝。