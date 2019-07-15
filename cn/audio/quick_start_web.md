# 快速开始

音频通信需要登录后并成功加入组，详见[加入组](../platform/prepare_web.md)。

## 广播音频

startPublishAudio()广播本地视频：

```js
webRtcEngine.startPublishVideo().then(() => {
     console.log('发布视频频成功')
})
```

音频广播后，组内所有用户会收到音频广播事件。

## 接听远端音频

通过receiveRemoteVideo,receiveRemoteAudio方法可以订阅远程的音视频流，参数为onPublisher事件返回的userId, mediaId。

```js
webRtcEngine.receiveRemoteAudio(userId, mediaId).then(()=>{
    console.log('订阅音频成功')
   },(error)=>{
       console.log(error.message);
 })
```

## 停止接听远端音频

当不需要订阅远程的流是，可以调用取消订阅方法，参数为onPublier 返回的userId, mediaId

```js
webRtcEngine.stopReceiveRemoteAudio(userId, mediaId).then(()=>{
    console.log('取消订阅音频成功')
   },(error)=>{
       console.log(error.message);
 })
```