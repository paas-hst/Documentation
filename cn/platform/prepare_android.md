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

使用SDK之前必须初始化。

```js
FspEngine fspEngine = FspEngine.createsApplication, appId, null, this);
fspEngine.init();
```

> 需要注意，引擎是单例，一个进程只能有一个实例，重复初始化可能会引起未知异常。

## 登录平台

初始化完成后，就可以登录平台了，登录需要使用到Token和User ID。其中，Token为字符串，用来校验身份和鉴权，由开发者自己生成，具体请参考“平台介绍->基本概念->应用鉴权”；User ID也是字符串，由开发者定义，用来唯一标识一个用户，开发者必须保证App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```js
fspEngine.login(token, userId);
```

> User ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

可以通过onLoginResult回调获得登录结果。


## 加入分组

登录成功后，绝大多数情况下，你需要加入分组，原因是平台的很多服务都是基于分组来提供的。Group ID也是由开发者自己定义，但必须确保App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```java
fspEngine.joinGroup(groupId);
```

> Group ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

可以通过onJoinGroupResult回调获得加入分组结果。

## 组成员通知
加入分组后，可以通过onGroupUsersRefreshed回调来获取分组成员列表，这个回调只会在加入分组时回调一次，推送全量用户列表。后续分组内成员列表的更新：加入和离开，会通过onRemoteUserEvent回调来通知上层应用，开发者可以基于这两个回调来实时维护分组内用户列表。