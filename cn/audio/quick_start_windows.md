# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

## 广播本地音频

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

```js
pEngine->StartPublishAudio()
```

> SDK会设置一个默认麦克风设备，如果想选择麦克风设备，请参考“进阶教程”。

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```js
pEngine->StopPublishAudio()
```

## 接听远端音频

收到广播音频事件后，便可以调用 MuteRemoteAudio 接口开始接听指定远端用户的音频。

```js
pFspEngine->MuteRemoteAudio(szUserId, false);
```

> 开发者可以通过设置FspEngineContext::auto_open_remote_audio参数决定是否默认接听。SDK内部默认会自动接听远端音频，此时还会收到远端广播音频事件，但可以不用手动调用接听音频的接口。

## 停止接听远端音频

在通信过程中，可以通过调用 MuteRemoteAudio 方法关闭远端音频。

```js
pFspEngine->MuteRemoteAudio(szUserId, true);
```

> 如果远端音频处于广播状态，再次调用 MuteRemoteAudio(szUserId, false) 又可以重新接听远端音频。