# 快速开始

使用屏幕共享服务前，请确保已经加入分组，具体请参考“准备工作”。


## 开始屏幕共享

开始采集桌面图像，分组内所有远端用户都会收到开始屏幕共享的事件。

```js
hstRtcEngine.startScreenShare();
```

## 停止屏幕共享

停止采集桌面图像，分组内所有远端用户都会收到停止屏幕共享的事件。

```js
hstRtcEngine.stopScreenShare();
```


## 接收屏幕共享

需要订阅“onPublishMedia”事件和“onRemoteMediaAdd”事件。收到“onPublishMedia”事件后，调用“startRecvScreenShare”接口开始接收远端屏幕共享流；收到“onRemoteMediaAdd”事件后，调用“setScreenShareRender”接口查看远端屏幕共享。

```js
// 订阅"onPublishMedia"事件，开始接收远端屏幕共享
hstRtcEngine.on('onPublishMedia', function (data) {
    if (data.mediaType == 0) { // 屏幕共享	
        hstRtcEngine.startRecvScreenShare(data.userId, data.mediaId)
        .then(() => {
            console.log("Start receive user " + data.userId + " screen share! ");
        })
        .catch(() => {
            console.log("Receive remote screen share failed!");
        })
    } 
}

// 订阅“onRemoteMediaAdd”事件，查看远端屏幕共享
hstRtcEngine.on('onRemoteMediaAdd', function (data) {
    if (data.mediaType == 0){ // 屏幕共享
        let videoElement = document.getElementById('screen-share-panel');
        hstRtcEngine.setScreenShareRender(videoElement, data.mediaId, data.userId);
    }
});

```


## 停止接收屏幕共享

通信的过程中，可以通过调用stopRecvScreenShare随时停止接收屏幕共享流。

一般情况，开发者需要订阅“onUnPublishMedia”事件，收到事件后，调用stopRecvScreenShare停止接收屏幕共享流。

```js
hstRtcEngine.on("onUnPublishMedia", function(data) {
    if (data.mediaType == 0) { // 屏幕共享
        hstRtcEngine.stopRecvScreenShare(data.userId, data.mediaId)
        .then(() => {
            console.log("Stop receive screen share.");
        })
        .catch(() => {
            console.log("Stop receive remote screen share failed!");
        })
    }
}
```