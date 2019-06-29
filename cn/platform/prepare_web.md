# 准备工作
在创建并初始化 HstRtcEngine 对象前，请确保你已完成环境准备、安装包获取等步骤。

## 初始化
Token用来进行登录认证，为保证账号的安全性，Token应该在开发者服务器端生成，

[点此下载](http://paas.hst.com/developer/downloadToken)Token生成代码

```js
  let webRtcEngine = new HstRtcEngine()
  let appId = "you app id" // 系统为应用分配的 APP ID
  let token = "you token"  // token
  webRtcEngine.init(appId, token)
```

## 加入组

指定Group ID和User ID加入分组，Group ID和User ID由开发者定义。开发者要保证在同一分组中User ID不会冲突，同一分组下相同的User ID，后加入的会被拒绝掉。

```js
  webRtcEngine.joinGroup(groupId, userId).then(() => {
      console.log('加入组成功')
  })
```