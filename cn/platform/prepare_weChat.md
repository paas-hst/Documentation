# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件

请确保满足以下开发环境要求:

- 安装Chrome 75+浏览器
- 确保部署环境为localhost或https协议
- 请确保已安装 微信开发者工具。
- 请确保你的微信小程序基础库支持 live-pusher 及 live-player 组件，且这两个组件在微信开发者工具中打开。
- 请确保在微信公众平台账号的开发设置中，给予以下域名请求权限：
  ```http
  request合法域名:
  https://access.paas.hst.com
  https://fspwxlite.hst.com
  https://fspwxlite.hst.com:443
  https://official.opensso.tencent-cloud.com
  https://paas-token-gen.haoshitong.com

  socket合法域名:
  wss://fsp-wxgw1.hst.com:50001
  wss://fsp-wxgw2.hst.com:50001
  wss://fsp-wxgw3.hst.com:50001
  wss://fsp-wxgw4.hst.com:50001
  wss://fsp-wxgw5.hst.com:50001
  wss://fsp-wxgw6.hst.com:50001
  wss://fsp-wxgw7.hst.com:50001
  wss://fsp-wxgw8.hst.com:50001
  wss://fsp-wxgw9.hst.com:50001
  wss://fspwxlite.hst.com:50001
  ```
- 请确保在使用相关功能及服务前，已打开特定端口

## 添加 SDK

1. 下载 [Web SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。 
2. 将JS文件保存到你所操作的项目下。
3. 在项目相应的前端页面文件中，对JS文件进行引用。


## 初始化

使用SDK之前必须初始化。

```js
// 引擎初始化
wx.request({
  url: 'https://access.paas.hst.com/server/address?appType=2',
  header: {
    'Content-Type': 'application/json'
  },
  success: function (res) {
    this.$hstEngine = new HstWxEngine(res.data.result)
	$hstEngine.init(appID, appSecret, onSuccess, onFailure)
  }
})

```

## 加入分组


通过指定Group ID和User ID加入分组，Group ID和User ID由开发者定义，开发者要保证同一App下Group ID和User ID不会冲突。具体请参考“平台介绍->基本概念->Group ID和User ID”。


```js
$hstEngine.join(isCreator, groupID, userID, onSuccess, onFailure)
```

> User ID和Group ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

