# 快速开始

本章演示如何快速发起屏幕共享和接收远端屏幕共享。


## 开始屏幕共享

开始采集桌面图像，分组内所有远端用户都会收到开始屏幕共享的事件。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.startPublishMedia(MediaType.SCREEN_SHARE);
```

开启屏幕共享后，可以显示本端屏幕共享画面，不过一般场景不需要显示本地共享的画面。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.setMediaRender(
	userId, // 本地登录userId 
	MediaType.SCREEN_SHARE, 
	null, 
	videoElement);
```

## 停止屏幕共享

停止采集桌面图像，分组内所有远端用户都会收到停止屏幕共享的事件。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.stopPublishMedia(MediaType.SCREEN_SHARE);
```

停止屏幕共享后，取消显示本端屏幕共享画面。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.unsetMediaRender(
	userId, // 本地登录userId
	MediaType.SCREEN_SHARE,
	videoElement);
```

## 接收远端屏幕共享

订阅“onPublishMedia”事件和“onRemoteMediaAdd”事件，收到“onPublishMedia”事件后，调用“startReceiveMedia”接口开始接收远端屏幕共享流；收到“onRemoteMediaAdd”事件后，调用“setMediaRender”接口查看远端屏幕共享画面。

```js
const MediaType = hstRtcEngine.MediaType;

// 订阅"onPublishMedia"事件，开始接收远端屏幕共享
hstRtcEngine.subEvent('onPublishMedia', function (data) {
    if (data.mediaType == MediaType.SCREEN_SHARE) {	
        hstRtcEngine.startReceiveMedia(data.userId, data.mediaType, data.mediaId)
        .then(() => {
            console.log("Start receive user " + data.userId + " screen share! ");
        })
        .catch(() => {
            console.log("Receive remote screen share failed!");
        })
    } 
}

// 订阅“onRemoteMediaAdd”事件，查看远端屏幕共享
hstRtcEngine.on('onRemoteMediaAdd', function (data) {
    if (data.mediaType == MediaType.SCREEN_SHARE){
        hstRtcEngine.setMediaRender(
			data.userId,
			data.mediaType,
			data.mediaId,
			document.getElementById('screen-share-panel'));
    }
});

```

## 停止接收远端屏幕共享

开发者可以通过调用stopReceiveMedia随时停止接收远端屏幕共享流。典型场景，开发者订阅“onUnPublishMedia”事件，收到事件后，调用stopReceiveMedia停止接收屏幕共享流，并调用unsetMediaRender取消显示远端屏幕共享画面。

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.on("onUnPublishMedia", function(data) {
    if (data.mediaType == MediaType.SCREEN_SHARE) {
        hstRtcEngine.stopReceiveMedia(data.userId, data.mediaType, data.mediaId)
        .then(() => {
            console.log("Stop receive screen share.");
            hstRtcEngine.unsetMediaRender(data.userId, data.mediaType, videoElement);
        })
        .catch(() => {
            console.log("Stop receive remote screen share failed!");
        })
    }
}
```