# 高级功能

## 前后切换
通过 switchCamera 方法可以在切换摄像头之间相互切换。isFrontCamera 方法确定当前摄像头是哪个。默认使用前置摄像头。

## 视频渲染拉伸模式

视频渲染支持3种拉伸模式：缩放平铺、等比裁剪、等比居中。

目前只有远端视频支持设置拉伸模式：

```java
fspEngine.setRemoteVideoRender(userId, videoId, renderView, mode);

//mode定义在 FspEngine 类：
public static final int RENDER_MODE_SCALE_FILL = 1; ///<缩放平铺
public static final int RENDER_MODE_CROP_FILL = 2;  ///<等比裁剪显示
public static final int RENDER_MODE_FIT_CENTER = 3; ///<等比居中显示
```

其中 userId videoId renderView 参数不变， 只改变第4个 mode 参数为希望的拉伸模式。


## 设置广播视频参数

广播端通过 setVideoProfile 方法设置视频相关参数：

```java
VideoProfile profile = new VideoProfile(1280, 720, 15);
fspEngine.setVideoProfile(profile);
```

应用设置的参数是目标值，SDK内部会根据摄像头支持的分辨率，接收端的网络情况等因素，自动微调视频参数。

## 获取远端视频参数

接收端可以定时调用 GetVideoStats 方法获取远端视频的参数信息：宽高，帧率，码率信息。