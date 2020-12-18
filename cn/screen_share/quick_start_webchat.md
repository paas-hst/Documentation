# 快速开始

本章演示如何接收远端屏幕共享（暂不支持小程序端共享屏幕），屏幕共享在微信小程序端也是一路视频，因此，接收屏幕共享和接收视频的逻辑和接口是一样的。


## 查看远端屏幕共享

订阅“onPublishMedia”事件，收到“onPublishMedia”事件后，调用“startReceiveMedia”接口开始接收远端屏幕共享；同时，需要根据视频数量（视频和屏幕共享总数量）调整webrtc-room组件的布局，webrtc-room组件会自动接收房间内的视频。

```js
const MediaType = hstRtcEngine.MediaType;

// 订阅"onPublishMedia"事件，开始接收远端屏幕共享
hstRtcEngine.subEvent('onPublishMedia', function (data) {
    if (data.mediaType == MediaType.SCREEN_SHARE) {
        hstRtcEngine.startReceiveMedia(data.userId, data.mediaType, data.mediaId)
        .then(() => {
            console.log("Start receive user " + data.userId + " screen share.");
        })
        .catch(() => {
            console.log("Receive remote screen share failed!");
        })
    } 
}

```

## 停止查看远端屏幕共享

订阅“onUnPublishMedia”事件，收到事件后，调用“stopReceiveMedia”接口停止接收远端屏幕共享；同时，需要根据视频数量调整webrtc-room组件的布局，webrtc-room组件会自动停止接收房间内的视频。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.subEvent("onUnPublishMedia", function(data) {
    if (data.mediaType == MediaType.SCREEN_SHARE) {
        hstRtcEngine.stopReceiveMedia(data.userId, data.mediaType, data.mediaId)
        .then(() => {
            console.log("Start receive remote screen share success.");
        })
        .catch(() => {
            console.log("Stop receive remote screen share failed!");
        })
    }
}
```