# 快速开始

视频通信需要登录后并成功加入组。

## 预览本地视频

通过调用如下代码添加预览窗口:

```js
let params = {
    audio: true,  // 音频打开
    video: true   // 视频打开
}
webRtcEngine.getLocalStream(params).then((stream) => {
  let video = document.getElementById('myPreView')
  console.log(stream)
  video.srcObject = obj.stream
})
```

## 广播视频

如果需要让远程订阅本地的视频流，需要调用startPublishVideo接口，发布本地流，远程会接收到onPublisher事件：

```js
webRtcEngine.startPublishVideo().then(() => {
     console.log('发布视频频成功')
})
```

视频广播后，组内所有用户会收到视频广播事件。

## 查看远端视频

通过receiveRemoteVideo方法可以订阅远程的音视频流，参数为onPublisher事件返回的userId, mediaId。

```js
 webRtcEngine.receiveRemoteVideo(userId, mediaId).then(()=> {
    console.log('订阅视频成功')
   },(error)=>{
       console.log(error.message);
 })
```

订阅成功到和远程人员建立链接是一个异步的过程，需要订阅onStreamUpdate事件，得到远程流的stream对象，通过video元素播放。

```js
 webEngine.on('onStreamUpdate', function (event) {
   if(event.type === 'audio') {
        dealAudio(event.stream)     
   } else if(event.type="video") {
        dealVideo(event)
   }
})
function dealVideo(stream){
    if(!$('#video' + stream.userId).get(0)) {
      var video = document.createElement("video");
      video.id = stream.userId
      video.setAttribute('autoplay','true')
      video.setAttribute('width','320')
      video.setAttribute('height', '320')
      video.srcObject = stream.stream
      document.getElementsByTagName('body')[0].appendChild(video)
    } else {
      $('#' + stream.userId).get(0).srcObject = stream.stream
    }
}
```

注：同一用户的音视频分为两个流

## 停止查看远端视频

当不需要订阅远程的流是，可以调用取消订阅方法，参数为 onPublier 返回的userId, mediaId

```js
webRtcEngine.stopReceiveRemoteVideo(userId, mediaId).then(()=> {
  console.log('取消订阅视频成功')
  },(error)=>{
      console.log(error.message);
})
```
