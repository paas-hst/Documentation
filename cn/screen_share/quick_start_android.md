# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。

> 当前Android端只支持接收远端屏幕共享，不支持将本端桌面共享出去。

## 接收屏幕共享


收到开始共享桌面的事件（OnRemoteVideoEvent），只需要设置视频窗口，SDK内部会自动接收屏幕共享视频流并将视频渲染到窗口上。

```js
fspEngine.setRemoteVideoRender(userId, videoId, renderView, renderMode);
```

> 屏幕共享服务和视频通信服务使用的是相同的传输通道，远端开始屏幕共享后，本端收到的事件与视频通信一样，通过Video ID来区分是到底是广播视频还是屏幕共享，如果Video ID为 fsp::RESERVED_VIDEOID_SCREENSHARE，则表示是屏幕共享，否则为广播视频。


## 停止接受屏幕共享

通信的过程中，可以通过将视频窗口设为空来停止接收屏幕共享。

```js
fspEngine.setRemoteVideoRender(userId, videoId, null, render_mode);
```

> Video ID为fsp::RESERVED_VIDEOID_SCREENSHARE。