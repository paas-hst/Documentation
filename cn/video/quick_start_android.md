# 快速开始

视频通信需要登录后并成功加入组，详见[加入组](../platform/prepare_windows.md)。

## 预览本地视频

通过调用如下代码添加预览窗口:

```java
m_fspEngine.startPreviewVideo(surfaceView);
```

添加预览窗口后，SDK会打开对应视频设备并在对应窗口上渲染本地视频。

## 广播视频

调用StartPublishVideo广播本地视频：

```java
m_fspEngine.startPublishVideo();
```

需要再本地视频已经预览后，才能进行视频广播。

视频广播后，组内所有用户会收到视频广播事件。

## 查看远端视频

组内任何一端收到视频广播事件后，可以设置相关渲染窗口，查看远端视频：

```java
m_fspEngine.setRemoteVideoRender(userId, videoId, renderView, renderMode)
```

设置渲染窗口，SDK内部会自动去服务器接收对应的视频流并在对应窗口上渲染。

## 停止查看远端视频

如何需要停止查看远端视频，可以将渲染窗口设为空，SDK就会停止查看远端视频

```java
m_fspEngine.setRemoteVideoRender(userId, videoId, null, renderMode)
```