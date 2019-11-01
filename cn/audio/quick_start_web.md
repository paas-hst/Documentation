# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

## 获取设备列表

广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，可以根据需要进行选择。

```js
webRtcEngine.getMediaDevices()
.then((mediaDevs) => {
	for (const dev of mediaDevs.micDevs){
	    console.log("device name: " + dev.devName + " device ID: " + dev.devId);
	}
	
	for (const dev of mediaDevs.spkDevs){
	    console.log("device name: " + dev.devName + " device ID: " + dev.devId);
	}
	
	for (const dev of mediaDevs.camDevs){
	    console.log("device name: " + dev.devName + " device ID: " + dev.devId);
	}
})
.catch(err => {
    console.log("Load media device failed!", err);
});
```

## 广播本地音频

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

广播本地音频只需一行代码：

```js
webEngine.startPublishAudio();
```

SDK会选择一个默认麦克风设备，如果有多个麦克风设备，可以选择使用哪个麦克风设备

```js
webRtcEngine.chooseMicDevice(micDevId);
```

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```js
webRtcEngine.stopPublishAudio();
```

## 接收远端音频

订阅"onPublishMedia"事件，收到广播事件后，调用startReceiveRemoteAudio接口开始接收音频。

```js
webEngine.on('onPublishMedia', function (data) {
    if (data.mediaType == 1) { // 音频
        webEngine.startReceiveRemoteAudio(data.userId, data.mediaId)
        .then(() => {
            console.log("Start receive remote audio.");
        })
        .catch((err)=>{
            console.log("Receive remote audio failed!");
        })
    } 
});
```

## 停止接收远端音频

订阅“onUnPublishMedia”事件，收到停止广播事件后，调用stopReceiveRemoteAudio停止接收音频。

```js
webEngine.on("onUnPublishMedia", function(data) {
    if (data.mediaType == 1) { // 音频
        webEngine.stopReceiveRemoteAudio(data.userId, data.mediaId)
        .then(() => {
            console.log("Stop receive remote audio.");
        })
        .catch(()=>{
            console.log("Stop receive remote audio failed!");
        })
    }
});
```

> 如果远端音频处于广播状态，再次调用 receiveRemoteAudio 又可以重新接听远端音频。
