# 高级功能

## 选择麦克风

系统中存在多个麦克风，但是又没有显示指定使用哪个麦克风，SDK会自动选择一麦克风设备。

开发者可以调用以下接口选择使用指定的麦克风设备。

```js
webRtcEngine.chooseMicDevice(micDevId);

```


