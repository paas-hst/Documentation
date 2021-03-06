# 快速开始

本章用来演示如何快速广播本地麦克风和接收远端音频。


## 获取设备列表

调用getMediaDevices获取本地麦克风和扬声器设备。

```js
hstRtcEngine.getMediaDevices()
.then((mediaDevs) => {
    // 麦克风设备
    for (const dev of mediaDevs.micDevs){
        console.log("device name: " + dev.devName + " device ID: " + dev.devId);
    }

    // 扬声器设备
    for (const dev of mediaDevs.spkDevs){
        console.log("device name: " + dev.devName + " device ID: " + dev.devId);
    }
})
.catch(err => {
    console.log("Load media device failed!", err);
});
```

## 广播本地音频

调用startPublishMedia广播本地麦克风，分组内所有用户都会接收到广播事件。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.startPublishMedia(MediaType.AUDIO, deviceId, null);
```

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

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

## 播放远端音频

订阅"onRemoteMediaAdd"事件，收到事件后，调用setStreamRender接口播放远端音频，videoElement为video标签。

```js
const MediaType = hstRtcEngine.MediaType;
hstRtcEngine.subEvent('onRemoteMediaAdd', function (data) {
    if (data.mediaType == MediaType.AUDIO) {
		hstRtcEngine.setMediaRender(data.userId, MediaType.AUDIO, data.mediaId, videoElement)
    }
}
```

## 停止接收远端音频

订阅“onUnPublishMedia”事件，收到事件后，调用stopReceiveMedia停止接收远端音频，并调用unsetStreamRender停止播放远端音频。

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
