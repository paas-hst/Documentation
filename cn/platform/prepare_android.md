# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件

请确保满足以下开发环境要求:

- Android SDK API Level Level ≥ 17

- Android Studio 3.0 或以上版本

- App 要求 Android 4.1 或以上设备

## 添加 SDK

1.  下载 [Android SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2.  aar库拷贝到 app/libs 目录下
3.  app的gradle脚本中正确引用到aar库，比如：implementation(name: 'fsp_sdk', ext: 'aar')

现在你已经设置好了 Android Studio 开发环境，可以开始使用 Android SDK 了！

## 初始化
使用SDK的第一步是做初始化：

```java
FspEngine fspEngine = FspEngine.createsApplication, appId, null, this);
fspEngine.init();
```


## 登录
登录需要从生成的token, 和上层指定UserId：

```java
fspEngine.login(token, userId);
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

登录结果在 onLoginResult 方法回调，如果 login 直接返回失败，则不会收到登录回调。

关于token请参考 [token说明](./token.md)

## 加入组

登录成功后，调用加入组的方法即可加入组：

```java
fspEngine.joinGroup(groupId);
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

加入成功或失败的结果，通过回调 onJoinGroupResult 方法回调，如果 joinGroup 直接返回失败，则不会收到登录回调。

## 组成员通知
加入组后，组内有成员进入或离开，会通过 IFspEngineEventHandler.onRemoteUserEvent 回调通知上层；刚加入组时通过 IFspEngineEventHandler.onGroupUsersRefreshed 全量通知组内所有成员列表。