# 准备工作

好视通云通信平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件

请确保满足以下开发环境要求:

-   操作系统： Microsoft Windows 7+
-   编译器：Microsoft Visual C++ 2015+
-   开发环境：Microsoft Visual Studio 2015 （推荐）

## 添加 SDK

1.  下载 [Windows SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2.  将 `sdk/include` 目录添加到项目的 INCLUDE 目录下。
3.  将 `sdk/lib` 目录放入项目的 LIB 目录下，显示添加对 fsp_sdk.lib 的链接。 
4.  将 `sdk/bin` 下的 bin 文件复制到你的可执行文件所在的目录下。


## 初始化
使用SDK的第一步是做初始化：

```js
IFspEngine* pFspEngine = FspGetEngine();

FspEngineContext enginContext; 
enginContext.app_id = strAppId;
enginContext.log_path = "./";
enginContext.event_handler = this;

m_pFspEngine->Init(m_FspEnginContext);
```


## 登录
登录需要依赖生成的token, 和上层指定UserId：

```js
pFspEngine->Login(szToken, szUserId);
```

> UserId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_), 横杠(-)。

登录结果在 OnFspEvent 方法回调， 回调的 eventType == EVENT_LOGIN_RESULT。如果 Login 直接返回失败，则不会收到登录回调。

关于token请参考 [token说明](./token.md)

## 加入组

登录成功后，调用加入组的方法即可加入组：

```js
pFspEngine->JoinGroup(szGroupId);
```

> GroupId有一定限制：字符串长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

加入成功或失败的结果，通过回调 OnFspEvent 方法回调， 回调的 eventType == EVENT_JOINGROUP_RESULT。如果 JoinGroup 直接返回失败，则不会收到登录回调。

## 组成员通知
加入分组后，系统会通过 IFspEngineEventHandler::OnGroupUsersRefreshed 推送当前组内所有成员列表。后续，组内有成员进入或离开，会通过 IFspEngineEventHandler::OnRemoteUserEvent 回调通知上层，开发者可以藉此维护分组内的用户列表。