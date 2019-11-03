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

只需设置video标签元素和Media ID，其中video标签元素为渲染目标对象，Media ID为调用getMediaDevices接口获取的设备devId。

```js
let videoElement = document.getElementById('video-panel');
let mediaId = "camera1";
hstRtcEngine.setVideoRender(videoElement, mediaId);
```

## 广播本地视频

打开本地摄像头，并广播给分组内所有用户，分组内所有远端用户都会接收到广播事件。

```js
hstRtcEngine.startPublishVideo(mediaId);
```


## 查看远端视频

需要订阅“onPublishMedia”事件和“onRemoteMediaAdd”事件。收到“onPublishMedia”事件后，调用“startReceiveRemoteVideo”接口开始接收远端视频；收到“onRemoteMediaAdd”事件后，调用“setVideoRender”接口查看远端视频。

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
	    hstRtcEngine.setVideoRender(videoElement, data.mediaId, data.userId);
	}
});

```
