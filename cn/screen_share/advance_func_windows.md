# 进阶教程


## 区域共享

某些场景下，可能需要共享桌面的某个区域，而不是整个桌面。和共享桌面调用的接口相同，只是前四个参数不能填0，代之的是桌面区域的定义，分别为left, top, right, bottom四个值，全0是一个特殊区域，特指整个桌面。

```js
pFspEngine->StartPublishScreenShare(0, 0, 100, 200, SCREEN_SHARE_BIAS_QUALITY);
```

> 支持在屏幕共享的过程中，动态调整桌面区域，但不是重新共享的方式。


## 远程控制

远程控制分控制端和被控制端两个角色，Windows端既支持控制远端（前提是远端支持被控制），也支持被远端控制。
SDK内部已经实现了远程控制的申请和控制，上层应用只需调用接口即可。

### 控制端申请远程控制

指定远端User ID，调用接口发起远程控制申请。

```js
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_REQUEST);
```

### 被控制端收到远程控制请求

被控制端会收到 IFspEngineEventHandler::OnRemoteControlOperationEvent 回调，表示远端有人申请控制本端桌面。

### 处理远程控制请求

收到远程控制请求后，可以调用接口同意/拒绝，控制端会收到处理结果的回调。

```js
// 同意远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_ACCEPT);

// 拒绝远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_REJECT);
```
