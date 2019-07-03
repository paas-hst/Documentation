# 快速开始

音频通信需要登录后并成功加入组，详见[加入组](../platform/prepare_windows.md)。

## 广播音频

调用StopPublishAudio()广播本地视频：

```c++
pEngine->StartPublishAudio()
```

音频广播后，组内所有用户会收到音频广播事件。

## 接听远端音频

组内任何一端收到视频广播事件后，可以开始接听远端音频。
SDK内部默认会自动接听远端音频，初始化时可以配置是否默认接听，通过FspEngineContext::auto_open_remote_audio参数决定是否默认接听。
如果没设置默认接听，通过 MuteRemoteAudio 方法开始接听远端音频。

```c++
pFspEngine->MuteRemoteAudio(szUserId, false);
```

## 停止接听远端视频

如果音频通信过程中需要关闭远端某路音频，通过MuteRemoteAudio方法实现

```c++
pFspEngine->MuteRemoteAudio(szUserId, true);
```

需要重新接听再次通过 MuteRemoteAudio(szUserId, false) 接听。