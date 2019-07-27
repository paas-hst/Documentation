# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

## 广播本地音频

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

```objectivec
[fspEngine startPublishAudio];
```

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```objectivec
[fspEngine stopPublishAudio];
```

## 接听远端音频

收到广播音频事件后，便可以调用 muteRemoteAudio 接口开始接听指定远端用户的音频。

```objectivec
[fspEngine muteRemoteAudio:szUserId mute:false];
```

## 停止接听远端视频

在通信过程中，可以通过调用 muteRemoteAudio 方法关闭远端音频。

```objectivec
[fspEngine muteRemoteAudio:szUserId mute:false];
```

需要重新接听再次通过[fspEngine muteRemoteAudio:szUserId mute:false]接听。

> 如果远端音频处于广播状态，再次调用 muteRemoteAudio 又可以重新接听远端音频。
