# 高级功能

## 设备管理

mac平台可以支持同时管理多个摄像头，通过 getVideoDevices 方法可以获取到系统的所有摄像头，
每个摄像头由 camera_id 标识，视频的本地预览，广播都需要指定用哪个摄像头设备。

## 摄像头切换

已经广播出去的视频，可直接 通过 startPublishVideo 实时切换摄像头。

```objc
[fspEngine startPublishVideo:szVideoId cameraId:cameraId];
```

szVideoId 参数传广播的VideoId，nDeviceId为希望切换到的nDeviceId。

如果有另外一路广播占用了这个摄像头，则会切换失败，返回失败错误码。

## 视频渲染拉伸模式

视频渲染支持3种拉伸模式：缩放平铺、等比裁剪、等比居中。

1. 本地预览修改拉伸模式：

```objc
[fspEngine AddVideoPreview:nDeviceId renderView:hVideoWnd mode:eRenderMode];

//mode定义在 FspEngine 类：
FSP_RENDERMODE_SCALE_FILL = 1, ///<缩放平铺
FSP_RENDERMODE_CROP_FILL = 2,  ///<等比裁剪显示
FSP_RENDERMODE_FIT_CENTER = 3  ///<等比居中显示
```

其中 nDeviceId 和 hVideoWnd 参数不变， 只改变第3个 eRenderMode 参数为希望的拉伸模式。

2. 远端视频修改拉伸模式：

```objc
[fspEngine setRemoteVideoRender:szUserId videoId:szVideoId renderView:hVideoWnd mode:eRenderMode];
```

其中 szUserId、 szVideoId、和 hVideoWnd 参数不变， 只改变第4个 eRenderMode 参数为希望的拉伸模式。


## 设置广播视频参数

广播端通过 setVideoProfile 方法设置视频相关参数：

```objc
FspVideoProfile *profile = [[FspVideoProfile alloc] init];
profile.width = 1280;
profile.height = 720;
profile.framerate = 15;
[fspEngine setVideoProfile:szVideoId profile:profile];
```

应用设置的参数是目标值，SDK内部会根据摄像头支持的分辨率，接收端的网络情况等因素，自动微调视频参数。

## 获取远端视频参数
接收端可以定时调用 getVideoStats 方法获取远端视频的参数信息：宽高，帧率，码率信息。
