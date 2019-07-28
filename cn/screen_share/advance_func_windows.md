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

+ 控制端申请远程控制

指定远端User ID，调用接口发起远程控制申请。

```js
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_REQUEST);
```

+ 被控制端收到远程控制请求

被控制端会收到 IFspEngineEventHandler::OnRemoteControlOperationEvent 回调，表示远端有人申请控制本端桌面。

+ 处理远程控制请求

收到远程控制请求后，可以调用接口同意/拒绝，控制端会收到处理结果的回调。

```js
// 同意远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_ACCEPT);

// 拒绝远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_REJECT);
```

## 设置Qos模式

屏幕共享产品能够使用在很多行业和业务场景中，比如会议、教育、培训、医疗等，有些业务场景要求尽量保持画面质量的清晰，比如共享Word、Excel等相对静态场景；有些业务场景要求尽量保证画面的流畅，比如共享视频等相对动态的场景。
屏幕共享产品提供了两种QoS模式：画面质量优先和画面流畅优先，开发者可以根据业务场景特点手动设置。

```js
// 同意远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_ACCEPT);

// 拒绝远端桌面控制请求
pFspEngine->RemoteControlOperation("remoteUserId", fsp::REMOTE_CONTROL_REJECT);
```

```js
// 画面质量优先
pFspEngine->StartPublishScreenShare(0, 0, 100, 200, SCREEN_SHARE_BIAS_QUALITY);

// 画面流畅优先
pFspEngine->StartPublishScreenShare(0, 0, 100, 200, SCREEN_SHARE_BIAS_QUALITY);
```