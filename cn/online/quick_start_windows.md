# 快速开始

在线状态相关业务功能只需要登录后即可使用，无需加入组，详见[登录](../platform/prepare_windows.md)。
，IFspSignaling 接口通过 IFspEngine::GetFspSignaling 获取。

## 初始化

在线业务都通过 IFspSignaling 接口来调用，初始时需要向IFspSignaling注册回调实现对象。

```js
fsp::IFspSignaling* m_pFspSignaling = m_pFspEngine->GetFspSignaling();
m_pFspSignaling->AddEventHandler(this);
```

> 在线和透明消息都通过 IFspSignaling 接口调用，只需初始化一次。

## 刷新在线列表
登录后，通过 UserStatusRefresh 方法可以刷新到应用下所有登录在线的userId列表。
也可以指定刷新部分userId的在线信息。

```js
fsp::Vector<fsp::String> vecUserIds;
unsigned int nRequestId;
m_pFspSignaling->UserStatusRefresh(vecUserIds, &nRequestId); //vecUserIds为空表示刷新所有在线用户
```

服务器响应后，会通过 OnUsersStateRefreshed 方法回调用户列表。

## 邀请

登录后，可以发送邀请给指定用户，携带GroupId，这样多方可以通过邀请加入同一个Group。
邀请发出后，一般会再调用 IFspEngine::JoinGroup 先加入指定的组。
```js
fsp::Vector<fsp::String> vecUserIds;
vecUserIds.push_back("user1");
vecUserIds.push_back("user2");
m_pFspSignaling->Invite(vecUserIds, "gropuid", "hi, join please", &nInviteId);
m_pFspEngine->JoinGroup("gropuid");
```

邀请发送后，被邀请的用户会收到 OnInviteCome 的回调。

## 拒绝&接收

收到其他人的邀请后，可以弹出界面让用户选择接受后拒绝并调用相关接口。
如果接受邀请后，一般会再调用 IFspEngine::JoinGroup 加入指定的组。

```js
m_pFspSignaling->AcceptInvite("inviterUserId", nInviteId);
m_pFspEngine->JoinGroup("gropuid");
```

接受或拒绝发出后，邀请方会收到 OnInviteAccepted 或 OnInviteRejected 的回调。