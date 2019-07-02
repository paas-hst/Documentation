# 快速开始

屏幕共享需要登录后并成功加入组，详见[加入组](../platform/prepare_windows.md)。

## 开始桌面共享

共享端调用 StartPublishScreenShare 开始桌面共享:

```c++
pFspEngine->StartPublishScreenShare(0, 0, 0, 0, SCREEN_SHARE_BIAS_QUALITY);
```

开始共享后，组内其他用户会收到 OnRemoteVideoEvent 事件回调， eventType == REMOTE_VIDEO_EVENT_PUBLISHE_STARTED 。

## 停止共享

调用StopPublishVideo广播本地视频：

```c++
pFspEngine->StopPublishVideo();
```

停止共享后，组内其他用户会收到 OnRemoteVideoEvent 事件回调， eventType == REMOTE_VIDEO_EVENT_PUBLISHE_STOPED 。

## 接收屏幕共享

组内任何一端收到OnRemoteVideoEvent事件后，判断videoid是否等于 fsp::RESERVED_VIDEOID_SCREENSHARE ，
如果是这个videoid，表示是屏幕共享，然后调用 SetRemoteVideoRender 设置渲染窗口。

```c++
//szVideoId==fsp::RESERVED_VIDEOID_SCREENSHARE
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, hVideoWnd, eRenderMode);
```

设置渲染窗口，SDK内部就会开始接收并显示屏幕共享画面。

## 停止查看远端视频

如何需要停止查看远端视频，可以将渲染窗口设为空，SDK就会停止查看屏幕共享：

```c++
//szVideoId==fsp::RESERVED_VIDEOID_SCREENSHARE
pFspEngine->SetRemoteVideoRender(szUserId, szVideoId, NULL, eRenderMode);
```

## 区域共享
在开始共享或共享过程中，调用StartPublishScreenShare是可以指定共享的区域，SDK会自动调整共享区域，
已经共享的情况下，StartPublishScreenShare只会调整区域，不会重新共享。

## 远程控制
1. 接收端调用 IFspEngine::RemoteControlOperation("共享端userid", fsp::REMOTE_CONTROL_REQUEST) 申请远程控制。

2. 共享端收到 IFspEngineEventHandler::OnRemoteControlOperationEvent 回调，
然后调用IFspEngine::RemoteControlOperation("控制申请端userid", fsp::REMOTE_CONTROL_ACCEPT)接收申请，
或IFspEngine::RemoteControlOperation("控制申请端userid", fsp::REMOTE_CONTROL_REJECT)拒绝申请。