# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。


## 广播本地音频

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

```js
webRtcEngine.startPublishAudio().then(() => {
     console.log('发布音频成功')
})
```


## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```js
webRtcEngine.stopPublishAudio().then(() => {
     console.log('停止发布音频成功')
})
```


## 接听远端音频

收到广播音频事件后，便可以调用 receiveRemoteAudio 接口开始接听指定远端用户的音频。参数为 onPublier 返回的userId和mediaId。

```js
webRtcEngine.receiveRemoteAudio(userId, mediaId).then(()=>{
    console.log('订阅音频成功')
   },(error)=>{
       console.log(error.message);
 })
```


## 停止接听远端音频

在通信过程中，可以通过调用 stopReceiveRemoteAudio 方法关闭远端音频。参数为 onPublier 返回的userId和mediaId。

```js
webRtcEngine.stopReceiveRemoteAudio(userId, mediaId).then(()=>{
    console.log('取消订阅音频成功')
   },(error)=>{
       console.log(error.message);
 })
```

> 如果远端音频处于广播状态，再次调用 receiveRemoteAudio 又可以重新接听远端音频。
