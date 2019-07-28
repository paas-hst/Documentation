# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。


## 开始桌面共享

开始采集桌面图像，分组内所有远端用户都会收到开始共享桌面的事件，接口的前四个参数必须填0。

```js
pFspEngine->StartPublishScreenShare(0, 0, 0, 0, SCREEN_SHARE_BIAS_QUALITY);
```
> 前四个参数用来指定共享区域，全0标识共享整个桌面，如果想共享桌面的指定区域，具体请参考进阶教程。

> 第五个参数为屏幕共享服务的QoS（Quality of Service）模式，具体请参考进阶教程。


## 停止桌面共享

停止采集桌面图像，分组内所有远端用户都会收到停止广播视频的事件。

```js
pFspEngine->StopPublishVideo();
```

> 屏幕共享采用的是视频传输通道，因此很多事件与视频通信是相同的，但参数会有变化。


## 接收屏幕共享

收到开始共享桌面的事件，只需要设置视频窗口，SDK内部会自动接收屏幕共享视频流并将视频渲染到窗口上。

```js
//szVideoId==fsp::RESERVED_VIDEOID_SCREENSHARE
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, hVideoWnd, eRenderMode);
```

> 对于Windows端，收到OnRemoteVideoEvent回调后，判断videoId是否等于 fsp::RESERVED_VIDEOID_SCREENSHARE ，
如果是则表示是屏幕共享视频流。


## 停止接收屏幕共享

通信的过程中，可以通过将视频窗口设为空来停止接收屏幕共享。

```js
//szVideoId==fsp::RESERVED_VIDEOID_SCREENSHARE
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, NULL, eRenderMode);
```