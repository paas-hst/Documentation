# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

## 广播本地音频

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

```TYPESCRIPT
fspEngine.startPublishAudio()
```

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```TYPESCRIPT
fspEngine.stopPublishAudio()
```

## 接听远端音频

收到广播音频事件后，便可以调用 openRemoteAudio 接口开始接听指定远端用户的音频。

```js
fspEngine.openRemoteAudio(userId);
```

> 开发者可以通过设置FspEngine.init(autoOpenRemoteAudio: true)参数决定是否默认接听。SDK内部默认会自动接听远端音频，此时还会收到远端广播音频事件，但可以不用手动调用接听音频的接口。

## 停止接听远端视频

在通信过程中，可以通过调用 closeRemoteAudio 方法关闭远端音频。

```js
fspEngine.closeRemoteAudio(userId);
```

> 如果远端音频处于广播状态，再次调用 openRemoteAudio 又可以重新接听远端音频。
