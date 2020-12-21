# 快速开始

本章演示如何快速广播本地摄像头和接收远端视频。


## 广播本地视频

调用startPublishMedia接口，广播本地摄像头；同时，设置webrtc-room组件的enableCamera属性为true，打开本地摄像头。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.startPublishMedia(MediaType.VIDEO, deviceId);
```


## 停止广播本地视频

调用stopPublishMedia接口停止广播视频；同时，设置webrtc-room组件的enableCamera属性为false，关闭本地摄像头。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.stopPublishMedia(MediaType.VIDEO, deviceId);
```


## 查看远端视频

订阅“onPublishMedia”事件，收到“onPublishMedia”事件后，调用“startReceiveMedia”接口开始接收远端视频；同时，需要根据视频数量调整webrtc-room组件的布局，webrtc-room组件会自动接收房间内的视频。

```js
const MediaType = hstRtcEngine.MediaType;

// 订阅"onPublishMedia"事件，开始接收远端视频
hstRtcEngine.subEvent('onPublishMedia', function (data) {
    if (data.mediaType == MediaType.VIDEO) {
        hstRtcEngine.startReceiveMedia(data.userId, MediaType.VIDEO, data.mediaId)
        .then(() => {
            console.log("Start receive user " + data.userId + " video! ");
        })
        .catch(() => {
            console.log("Receive remote video failed!");
        })
    } 
}

```

## 停止查看远端视频

订阅“onUnPublishMedia”事件，收到事件后，调用“stopReceiveMedia”接口停止接收远端视频；同时，需要根据视频数量调整webrtc-room组件的布局，webrtc-room组件会自动停止接收房间内的视频。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.subEvent("onUnPublishMedia", function(data) {
    if (data.mediaType == MediaType.VIDEO) {
        hstRtcEngine.stopReceiveMedia(data.userId, MediaType.VIDEO, data.mediaId)
        .then(() => {
            console.log("Start receive remote video success.");
        })
        .catch(() => {
            console.log("Stop receive remote video failed!");
        })
    }
}
```