# 准备工作
请确保满足以下开发环境要求：
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

## 初始化
使用SDK的第一步是做初始化：

```
// 引擎初始化
wx.request({
  url: 'https://access.paas.hst.com/server/address?appType=2',
  header: {
    'Content-Type': 'application/json'
  },
  success: function (res) {
    this.$hstEngine = new HstWxEngine(res.data.result)
  }
})
```


## 获取试用权限
鉴权需要appID和appSecret：

```
$hstEngine.init(appID, appSecret, onSuccess, onFailure)
```

## 加入组
登录成功后，调用加入组的方法即可加入组：

```
$hstEngine.join(isCreator, groupID, userID, onSuccess, onFailure)
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。