# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。



## 接收屏幕共享

组内任何一端收到OnRemoteVideoEvent事件后，判断videoid是否等于 FspEngine.RESERVED_VIDEOID_SCREENSHARE ，
如果是这个videoid，表示是屏幕共享，然后调用 SetRemoteVideoRender 设置渲染窗口。

```js
//videoId==FspEngine.RESERVED_VIDEOID_SCREENSHARE
m_fspEngine.setRemoteVideoRender(userId, videoId, renderView, renderMode);
```

设置渲染窗口，SDK内部就会开始接收并显示屏幕共享画面。

## 停止查看远端视频

如何需要停止查看远端视频，可以将渲染窗口设为空，SDK就会停止查看屏幕共享：

```js
//videoId==FspEngine.RESERVED_VIDEOID_SCREENSHARE
m_fspEngine.setRemoteVideoRender(userId, videoId, null, render_mode);
```
