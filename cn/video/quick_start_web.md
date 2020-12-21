# 快速开始

本章演示如何快速广播本地摄像头和接收远端视频。


## 获取设备列表

调用getMediaDevices获取本地设摄像头设备。

```js
hstRtcEngine.getMediaDevices()
.then((mediaDevs) => {
    // 摄像头设备
    for (const dev of mediaDevs.camDevs){
        console.log("device name: " + dev.devName + " device ID: " + dev.devId);
    }
})
.catch(err => {
    console.log("Load media device failed!", err);
});
```

## 预览本地视频

设置video标签和设备ID，引擎会打开deviceId指定的摄像头，并将视频渲染到video标签对象。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.setMediaRender(
	userId, // 登录userId
	MediaType.VIDEO,
	deviceId,
	document.getElementById('video-panel'));
```

> deviceId为调用getMediaDevices接口获取的设备devId。


## 广播本地视频

打开本地摄像头，并广播给分组内所有用户，分组内所有远端用户都会接收到onPublishMedia事件。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.startPublishMedia(MediaType.VIDEO, deviceId);
```


## 停止广播本地视频

停止发送本地视频流，分组内所有远端用户都会收到onUnPublishMedia事件。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.stopPublishMedia(MediaType.VIDEO, deviceId);
```


## 查看远端视频

订阅“onPublishMedia”事件和“onRemoteMediaAdd”事件。收到“onPublishMedia”事件后，调用“startReceiveMedia”接口开始接收远端视频；收到“onRemoteMediaAdd”事件后，调用“setStreamRender”接口显示远端视频。

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

// 订阅“onRemoteMediaAdd”事件，查看远端视频
hstRtcEngine.subEvent('onRemoteMediaAdd', function (data) {
    if (data.mediaType == MediaType.VIDEO){
        let videoElement = document.getElementById('video-panel');
        hstRtcEngine.setMediaRender(data.userId, MediaType.VIDEO, data.mediaId, videoElement);
    }
});
```

## 停止查看远端视频

订阅“onUnPublishMedia”事件，收到事件后，调用“stopReceiveMedia”接口停止接收远端视频，同时，调用“unsetMediaRender”接口取消显示远端视频。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.subEvent("onUnPublishMedia", function(data) {
    if (data.mediaType == MediaType.VIDEO) {
        hstRtcEngine.stopReceiveMedia(data.userId, MediaType.VIDEO, data.mediaId)
        .then(() => {
            hstRtcEngine.unsetMediaRender(userId, MediaType.VIDEO, videoElement);
        })
        .catch(() => {
            console.log("Stop receive remote video failed!");
        })
    }
}
```