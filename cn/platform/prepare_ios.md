# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件
请确保满足以下开发环境要求:

- Xcode 10.0+
- iOS 8.0+ 真机(iPhone 或 iPad)
- 请确保您的项目已设置有效的开发者签名

## 添加SDK
1. 下载[iOS SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2. 使用 Xcode 打开你想要运行的项目，然后选中当前 Target。
3. General 页签,展开Embedded Binaries项,点击+图标添加FspKit.framework

<img alt="ios_integrate2" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/ios_Integrate2.png" align="center" />

4. Build Phases 页签，展开 Link Binary with Libraries 项并添加如下库。点击 + 图标开始添加

    + VideoToolbox.framework
    + MediaToolbox.framework
    + CoreAudio.framework
    + AudioToolbox.framework
    + CoreMedia.framework
    + AVFoundation.framework
    + libiconv.tbd
    + libz.tbd
    + libc++.tbd

<img alt="ios_integrate1" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/ios_Integrate.png" align="center" />



## 初始化

使用SDK之前必须初始化。

```objectivec
FspEngine *fspEngine = [FspEngine sharedEngineWithAppId:appId logPath:logPath serverAddr:serverAddr delegate:delegate];
```

> 需要注意，引擎是单例，一个进程只能有一个实例，重复初始化可能会引起未知异常。

## 登录

初始化完成后，就可以登录平台了，登录需要使用到Token和User ID。其中，Token为字符串，用来校验身份和鉴权，由开发者自己生成，具体请参考“平台介绍->基本概念->应用鉴权”；User ID也是字符串，由开发者定义，用来唯一标识一个用户，开发者必须保证App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```objectivec
[fspEngine login:szToken userId:szUserId];
```

> User ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

开发者可以通过 FspEngineDelegate::fspEvent 回调获得登录结果，事件类型（eventType）为 EVENT_LOGIN_RESULT。

> 如果 login 调用返回失败，则不会收到回调事件。


## 加入分组

登录成功后，绝大多数情况下，你需要加入分组，原因是平台的很多服务都是基于分组来提供的。Group ID也是由开发者自己定义，但必须确保App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```objectivec
[fspEngine joinGroup:szGroupId];
```

> Group ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

可以通过 FspEngineDelegate::fspEvent 回调获得加入分组结果，事件类型（eventType）为EVENT_JOINGROUP_RESULT。

> 如果 joinGroup 调用返回失败，则不会收到回调事件。

## 分组成员列表

加入分组后，可以通过 FspEngineSignalingDelegate::onGroupUsersRefreshed 回调来获取分组成员列表，这个回调只会在加入分组时回调一次，推送全量用户列表。后续分组内成员列表的更新：加入和离开，会通过 FspEngineSignalingDelegate::onGroupUserJoined 和 FspEngineSignalingDelegate::onGroupUserLeaved 回调来通知上层应用，开发者可以基于这两个回调来实时维护分组内用户列表。
