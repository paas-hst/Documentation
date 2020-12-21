# 快速开始

本文演示如何快速广播本地麦克风和接收远端音频。


## 广播本地音频

调用startPublishMedia开始广播本地麦克风；同时，设置webrtc-room组件的muted属性为false，打开本地麦克风。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.startPublishMedia(MediaType.AUDIO, deviceId, null);
```

## 停止广播本地音频

调用stopPublishMedia停止广播本地麦克风；同时，设置webrtc-room组件的muted属性为true，关闭本地麦克风。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.stopPublishMedia(MediaType.AUDIO);
```

## 接收远端音频

订阅"onPublishMedia"事件，收到事件后，调用startReceiveMedia接口开始接收远端音频。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.subEvent('onPublishMedia', function (data) {
    if (data.mediaType == MediaType.AUDIO) {
        hstRtcEngine.startReceiveMedia(data.userId, MediaType.AUDIO, data.mediaId)
        .then(() => {
            console.log("Start receive remote audio.");
        })
        .catch((err)=>{
            console.log("Receive remote audio failed!");
        })
    } 
});
```

> webrtc-room组件会自动播放远端音频。

## 停止接收远端音频

订阅“onUnPublishMedia”事件，收到事件后，调用stopReceiveMedia停止接收远端音频。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.subEvent("onUnPublishMedia", function(data) {
    if (data.mediaType == MediaType.AUDIO) {
        hstRtcEngine.stopReceiveMedia(data.userId, MediaType.AUDIO, data.mediaId)
        .then(() => {
			hstRtcEngine.unsetMediaRender(data, MediaType.AUDIO, videoElement)
            console.log("Stop receive remote audio.");
        })
        .catch(()=>{
            console.log("Stop receive remote audio failed!");
        })
    }
});
```

