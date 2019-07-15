# 准备工作
集成SDK后，需要2个或3个简单的准备动作：初始化，登录，加入组。
登录和加入组是两个动作，登录成功后才能加入组，大部分业务需要加入组后才能正常使用

## 初始化
使用SDK的第一步是做初始化：

```
IFspEngine* m_pFspEngine = FspGetEngine();
FspEngineContext enginContext;
enginContext.app_id = strAppId;
enginContext.log_path = "./";
enginContext.event_handler = this;
m_pFspEngine->Init(m_FspEnginContext);
```


## 登录
登录需要依赖生成的token, 和上层指定UserId：

```
pFspEngine->Login(szToken, szUserId);
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

登录结果在 OnFspEvent 方法回调， 回调的 eventType == EVENT_LOGIN_RESULT。如果 Login 直接返回失败，则不会收到登录回调。

关于token请参考 [token说明](./token.md)

## 加入组

登录成功后，调用加入组的方法即可加入组：

```
pFspEngine->JoinGroup(szGroupId);
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

加入成功或失败的结果，通过回调 OnFspEvent 方法回调， 回调的 eventType == EVENT_JOINGROUP_RESULT。如果 JoinGroup 直接返回失败，则不会收到登录回调。

## 组成员通知
加入组后，组内有成员进入或离开，会通过 IFspEngineEventHandler::OnRemoteUserEvent 回调通知上层；开始会通过 IFspEngineEventHandler::OnGroupUsersRefreshed 全量通知组内所有成员列表。