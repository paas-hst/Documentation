# 快速开始

使用视频通信服务前，请确保已经加入分组，具体请参考“准备工作”。


## 开始桌面共享

开始采集桌面图像，分组内所有远端用户都会收到开始共享桌面的事件，接口的前四个参数必须填0。

```js
pFspEngine->StartPublishScreenShare(0, 0, 0, 0, SCREEN_SHARE_BIAS_QUALITY);
```
> 前四个参数用来指定共享区域，全0表示共享整个桌面，共享桌面的指定区域请参考进阶教程。

> 第五个参数为屏幕共享服务的QoS（Quality of Service）模式，具体请参考进阶教程。


## 停止桌面共享

停止采集桌面图像，分组内所有远端用户都会收到停止广播视频的事件。

```js
pFspEngine->StopPublishVideo();
```


## 接收屏幕共享

收到开始共享桌面的事件，只需要设置视频窗口，SDK内部会自动接收屏幕共享视频流并将视频渲染到窗口上。

```js
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, hVideoWnd, eRenderMode);
```

> 屏幕共享服务和视频通信服务使用的是相同的传输通道，远端开始共享后，本端收到的事件与视频通信一样，通过Video ID来区分是到底是视频通信流还是屏幕共享流，如果Video ID为 fsp::RESERVED_VIDEOID_SCREENSHARE，则表示是屏幕共享流，否则为视频通信流。


## 停止接收屏幕共享

通信的过程中，可以通过将视频窗口设为空来停止接收屏幕共享。

```js
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, NULL, eRenderMode);
```

> Video ID为fsp::RESERVED_VIDEOID_SCREENSHARE。