# 快速开始

使用音频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

## 获取设备列表

<div style="font-family: Verdana,Arial,Helvetica,sans-serif;font-size: 20px; margin-top:10px">
广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。
广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。
广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。
</div>

广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。
广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。
广播本地音频时，需要指定麦克风设备，同时，也需要选择本地使用的扬声器设备。SDK提供一个接口同时获取摄像头、麦克风和扬声器设备，开发者可以根据需要进行选择。



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

打开本地麦克风，并广播给分组内所有用户，分组内所有用户都会接收到广播音频事件。

```js
hstRtcEngine.startPublishAudio();
```

## 停止广播本地音频

关闭本地麦克风，分组内所有用户都会接收到停止广播音频事件。

```js
hstRtcEngine.stopPublishAudio();
```

## 接收远端音频

订阅"onPublishMedia"事件，收到广播事件后，调用startReceiveRemoteAudio接口开始接收音频。

```js
hstRtcEngine.on('onPublishMedia', function (data) {
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
hstRtcEngine.on("onUnPublishMedia", function(data) {
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
