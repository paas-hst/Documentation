# 高级功能

## 摄像头切换
通过switchCamera方法可以在前置与后置摄像头之间相互切换。

## 视频渲染拉伸模式

视频渲染支持3种拉伸模式：缩放平铺、等比裁剪、等比居中。

目前只有远端视频支持设置拉伸模式：

```objectivec
[fspEngine setRemoteVideoRender:userId videoId:videoId render:renderView mode:mode];

//mode定义在 FspEngine 类：
FSP_RENDERMODE_SCALE_FILL = 1, ///<缩放平铺
FSP_RENDERMODE_CROP_FILL = 2,  ///<等比裁剪显示
FSP_RENDERMODE_FIT_CENTER = 3  ///<等比居中显示
```

其中 userId、 videoId、和 render 参数不变， 只改变第4个 mode 参数为希望的拉伸模式。


## 设置广播视频参数

广播端通过 setVideoProfile 方法设置视频相关参数：

```objectivec
FspVideoProfile *profile = [[FspVideoProfile alloc] init];
profile.width = 1280;
profile.height = 720;
profile.framerate = 15;
[fspEngine setVideoProfile:profile];
```

应用设置的参数是目标值，SDK内部会根据摄像头支持的分辨率，接收端的网络情况等因素，自动微调视频参数。

## 获取远端视频参数
接收端可以定时调用 getVideoStats 方法获取远端视频的参数信息：宽高，帧率，码率信息。
