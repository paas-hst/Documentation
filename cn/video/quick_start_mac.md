# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。


## 预览本地视频

只需设置视频预览窗口，便可以预览本地视频，SDK会打开对应视频设备并在对应窗口上渲染本地视频。

```objectivec
[fspEngine addVideoPreview:nDeviceId renderView:hVideoWnd mode:eRenderMode];
```

## 停止预览本地视频

将视频预览窗口设空，即可停止预览本地窗口。

```objectivec
[fspEngine addVideoPreview:nDeviceId renderView:nil mode:0];
```

> 第三个参数SDK内部不做校验。


## 广播本地视频

打开本地摄像头，并广播给分组内所有用户，分组内所有远端用户都会接收到广播视频事件。

```objectivec
[fspEngine startPublishVideo:szVideoId cameraId:nDeviceId];
```

> szVideoId参数的设置请参考“平台介绍->基本概念->Video ID”。


## 停止广播本地视频

关闭本地摄像头，分组内所有远端用户都会接收到停止广播视频事件。

```objectivec
[fspEngine stopPublishVideo:szVideoId cameraId:nDeviceId];
```


## 查看远端视频

收到远端广播视频事件后，只需要设置视频窗口，便可查看指定用户的视频，SDK内部会自动获取视频流并渲染到窗口上。

```objectivec
[fspEngine setRemoteVideoRender:szUserId videoId:szVideoId renderView:hVideoWnd mode:eRenderMode];
```


## 停止查看远端视频

在通信过程中，可以通过将视频窗口设空，来停止查看远端视频。

```objectivec
[fspEngine setRemoteVideoRender:szUserId videoId:szVideoId renderView:nil mode:eRenderMode];
```

> 如果远端视频处于广播状态，再次设置视频窗口又可以重新查看远端音频。