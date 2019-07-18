# 快速开始

音频通信需要登录后并成功加入组，详见[加入组](../platform/prepare_mac.md)。

## 广播音频

调用stopPublishAudio广播本地音频：

```objectivec
[fspEngine stopPublishAudio];
```

音频广播后，组内所有用户会收到音频广播事件。

## 接听远端音频

组内任何一端收到视频广播事件后，可以开始接听远端音频。
SDK内部默认会自动接听远端音频。
如果没设置默认接听，通过 muteRemoteAudio 方法开始接听远端音频。

```objectivec
[fspEngine muteRemoteAudio:szUserId mute:false];
```

## 停止接听远端视频

如果音频通信过程中需要关闭远端某路音频，通过muteRemoteAudio方法实现

```objectivec
[fspEngine muteRemoteAudio:szUserId mute:false];
```

需要重新接听再次通过[fspEngine muteRemoteAudio:szUserId mute:false]接听。
