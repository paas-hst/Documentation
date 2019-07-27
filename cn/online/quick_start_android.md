# 快速开始

在线状态相关业务功能只需要登录后即可使用，无需加入组，详见[登录](../platform/prepare_android.md)。

## 初始化

透明消息都通过 IFspSignaling 接口来调用，初始时需要向IFspSignaling注册回调实现对象。

```js
IFspSignaling fspSignaling = m_fspEngine.getFspSignaling();
fspSignaling.addEventHandler(this);
```

## 刷新在线列表
登录后，通过 refreshAllUserStatus 方法可以刷新到应用下所有登录在线的userId列表。
也可以通过refreshUserStatus指定刷新部分userId的在线信息。

```js
m_fspEngine.getFspSignaling().refreshAllUserStatus();
```

服务器响应后，会通过 IFspSignalingEventHandler.onRefreshUserStatusFinished 方法回调用户列表。

## 邀请

登录后，可以发送邀请给指定用户，携带GroupId，这样多方可以通过邀请加入同一个Group。
邀请发出后，一般会再调用 FspEngine.joinGroup 先加入指定的组。
```js
m_fspEngine.getFspSignaling().invite(userIds, groupId, msg);
m_fspEngine.joinGroup("gropuid");
```

邀请发送后，被邀请的用户会收到 IFspSignalingEventHandler.onInviteIncome 的回调。

## 邀请拒绝&接收

收到其他人的邀请后，可以弹出界面让用户选择接受后拒绝并调用相关接口。
如果接受邀请后，一般会再调用 FspEngine.joinGroup 加入指定的组。

```js
m_fspEngine.getFspSignaling().acceptInvite("inviterUserId", nInviteId);
m_fspEngine.joinGroup("gropuid");
```

接受或拒绝发出后，邀请方会收到 onInviteAccepted 或 onInviteRejected 的回调。