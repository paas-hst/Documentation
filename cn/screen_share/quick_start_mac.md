# 快速开始

屏幕共享需要登录后并成功加入组，详见[加入组](../platform/prepare_mac.md)。

目前Mac只支持接收屏幕共享

## 接收屏幕共享

组内任何一端收到FspEngineDelegate::remoteVideoEvent事件后，判断videoid是否等于 FSP_RESERVED_VIDEOID_SCREENSHARE ，
如果是这个videoid，表示是屏幕共享，然后调用 setRemoteVideoRender 设置渲染窗口。

```objectivec
//videoId == FSP_RESERVED_VIDEOID_SCREENSHARE
[fspEngine setRemoteVideoRender:userId videoId:videoId render:renderView mode:renderMode];
```

设置渲染窗口，SDK内部就会开始接收并显示屏幕共享画面。

## 停止查看远端视频

如何需要停止查看远端视频，可以将渲染窗口设为空，SDK就会停止查看屏幕共享：

```objectivec
//videoId== FSP_RESERVED_VIDEOID_SCREENSHARE
[fspEngine setRemoteVideoRender:userId videoId:videoId render:nil mode:renderMode];
```
