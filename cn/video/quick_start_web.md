# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。


## 获取设备列表

广播本地摄像头，需要指定摄像头设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。

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
let videoElement = document.getElementById('video-panel');
let mediaId = "camera1";
hstRtcEngine.setVideoRender(videoElement, deviceId);
```

> deviceId为调用getMediaDevices接口获取的设备devId。


## 广播本地视频

打开本地摄像头，并广播给分组内所有用户，分组内所有远端用户都会接收到onPublishMedia事件。

```js
hstRtcEngine.startPublishVideo(deviceId);
```


## 停止广播本地视频

停止发送本地视频流，分组内所有远端用户都会收到onUnPublishMedia事件。

```js
hstRtcEngine.stopPublishVideo(deviceId);
```


## 查看远端视频

订阅“onPublishMedia”事件和“onRemoteMediaAdd”事件。收到“onPublishMedia”事件后，调用“startReceiveRemoteVideo”接口开始接收远端视频；收到“onRemoteMediaAdd”事件后，调用“setStreamRender”接口显示远端视频。

```js
// 订阅"onPublishMedia"事件，开始接收远端视频
hstRtcEngine.on('onPublishMedia', function (data) {
    if (data.mediaType == 2) { // 视频	
        hstRtcEngine.startReceiveRemoteVideo(data.userId, data.mediaId)
        .then(() => {
            console.log("Start receive user " + data.userId + " video! ");
        })
        .catch(() => {
            console.log("Receive remote video failed!");
        })
    } 
}

// 订阅“onRemoteMediaAdd”事件，查看远端视频
hstRtcEngine.on('onRemoteMediaAdd', function (data) {
    if (data.mediaType == 2){ // 视频
        let videoElement = document.getElementById('video-panel');
        hstRtcEngine.setStreamRender(videoElement, data.mediaId, data.userId);
    }
});

```

## 停止查看远端视频

订阅“onUnPublishMedia”事件，收到事件后，调用“stopReceiveRemoteVideo”接口停止接收远端视频，同时，调用“unsetStreamRender”接口取消显示远端视频。

```js
hstRtcEngine.on("onUnPublishMedia", function(data) {
    if (data.mediaType == 2) { // 视频
        hstRtcEngine.stopReceiveRemoteVideo(data.userId, data.mediaId)
        .then(() => {
            hstRtcEngine.unsetStreamRender(videoElement, streamId);
        })
        .catch(() => {
            console.log("Stop receive remote video failed!");
        })
    }
}
```