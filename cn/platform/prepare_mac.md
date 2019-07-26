# 准备工作
好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件
请确保满足以下开发环境要求:

- Xcode 10.0+
- mac OS 10.11+
- 请确保您的项目已设置有效的开发者签名

## 添加SDK
1. 下载[Mac SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。

2. 使用 Xcode 打开你想要运行的项目，然后选中当前 Target。
3. Build Phases 页签，展开 Link Binary with Libraries 项并添加如下库。点击 + 图标开始添加

+ VideoToolbox.framework
+ CoreAudio.framework
+ AudioToolbox.framework
+ CoreMedia.framework
+ VideoDecodeAcceleration.framework
+ libiconv.tbd
+ libz.tbd
+ libc++.tbd

<img alt="mac_integrate" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/mac_Integrate.png" align="center" />


## 初始化
使用SDK的第一步是做初始化：

```objectivec
FspEngine *fspEngine = [FspEngine sharedEngineWithAppId:appId logPath:logPath serverAddr:serverAddr delegate:delegate];
```


## 登录
登录需要从生成的token, 和上层指定UserId：

```objectivec
[fspEngine login:szToken userId:szUserId];
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

登录结果在 FspEngineDelegate::fspEvent  方法回调， 回调的 eventType == EVENT_LOGIN_RESULT。如果 login 直接返回失败，则不会收到登录回调。


## 加入组

登录成功后，调用加入组的方法即可加入组：

```objectivec
[fspEngine joinGroup:szGroupId];
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

加入成功或失败的结果，通过回调 FspEngineDelegate::fspEvent  方法回调， 回调的 eventType == EVENT_JOINGROUP_RESULT。如果 joinGroup 直接返回失败，则不会收到登录回调。

## 组成员通知
加入组后，组内有成员进入或离开，会通过 FspEngineSignalingDelegate::onGroupUserJoined,onGroupUserLeaved 回调通知上层；开始会通过 FspEngineSignalingDelegate::onGroupUsersRefreshed 全量通知组内所有成员列表。
