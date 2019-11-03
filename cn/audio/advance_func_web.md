# 高级功能

此文展示音频通信相关高级功能。

## 选择麦克风

系统中存在多个麦克风，但是又没有显示指定使用哪个麦克风，SDK会自动选择一麦克风设备。

开发者可以调用以下接口选择使用指定的麦克风设备。

```js
webRtcEngine.chooseMicDevice(micDevId);

```


## 获取音频流统计

如果想获取音频流的码流大小，可以使用getStats接口。

```js
webRtcEngine.getStats(options);

let stats = hstRtcEngine.getStats({userId: "xxx", mediaType: 1, mediaId: "xxx"});
if (stats) {
    console.log("Audio bitrate = " + stats.audio.bitRate);
}

```

此接口获得音频bitRate单位是kbps，获取后可以直接显示，如果想获取实时音频码流，使用定时器定时调用此接口即可。