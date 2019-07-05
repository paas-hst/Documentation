# 快速开始

在线状态相关业务功能只需要登录后即可使用，无需加入组，详见[登录](../platform/prepare_ios.md)。

## 初始化

在线业务都通过 FspEngine 接口来调用，初始时需要向FspEngine注册回调代理实现对象。

```objc
FspEngine *fspEngine = [FspEngine sharedEngineWithAppId:appId logPath:logPath serverAddr:serverAddr delegate:delegate];
```

> 业务消息都通过 FspEngine 接口调用，只需初始化一次。

## 刷新在线列表
登录后，通过 userStatusRefresh 方法可以刷新到应用下所有登录在线的userId列表。
也可以指定刷新部分userId的在线信息。

```objc
unsigned int nRequestId;
//vecUserIds为空表示刷新所有在线用户
[fspEngine userStatusRefresh:vecUserIds requestId:&nRequestId];
```

服务器响应后，会通过 FspEngineSignalingDelegate::refreshUserStatusFinished 方法回调用户列表。

## 邀请

登录后，可以发送邀请给指定用户，携带GroupId，这样多方可以通过邀请加入同一个Group。
邀请发出后，一般会再调用 FspEngine::joinGroup 先加入指定的组。

```objc
unsigned int nRequestId;
[fspEngine inviteUser:vecUserIds groupId:groupid extraMsg:"hi, join please" inviteId:&nRequestId];

[fspEngine joinGroup:nGroupId];
```

邀请发送后，被邀请的用户会收到 FspEngineSignalingDelegate::onInviteIncome 的回调。

## 拒绝&接收

收到其他人的邀请后，可以弹出界面让用户选择接受后拒绝并调用相关接口。
如果接受邀请后，一般会再调用 FspEngine::joinGroup 加入指定的组。

```objc
[fspEngine acceptInvite:nInviteUserId inviteId:nInviteId];

[fspEngine joinGroup:groupid];
```

接受或拒绝发出后，邀请方会收到 FspEngineSignalingDelegate::onInviteAccepted 或 FspEngineSignalingDelegate::onInviteRejected 的回调。
