
## API列表
| 接口 | 描述 |
| - | - |
| init | 初始化RTC引擎 |
| login | 登录平台 |
| joinGroup | 加入分组 |
| leaveGroup | 离开分组 |
| exit | 退出登录 |
| destroy | 销毁引擎 |
| on | 订阅事件 |
| startPublishVideo | 广播本地视频 |
| stopPublishVideo | 停止广播本地视频 |
| setLocalVideoRender | 设置本地视频渲染对象 |
| unsetLocalVideoRender | 取消设置本地视频渲染对象 |
| startReceiveRemoteVideo | 接收远端视频 |
| stopReceiveRemoteVideo | 停止接收远端视频 |
| setStreamRender | 设置远端媒体渲染对象 |
| unsetStreamRender | 取消设置远端媒体渲染对象 |
| getStats | 获取视频流统计数据 |
| getMediaDevices | 获取视频设备 |

## init

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```js
hstRtcEngine.init([accessUrl])
```


### 参数说明

accessUrl： Access服务URL地址。
  Access服务主要提供负载均衡功能，客户端需要访问Access服务来获取其他服务的地址。
  如果使用的公有云服务，则不需要传递此参数；如果使用的私有云服务，则需要设置此参数，具体传递规则请咨询技术人员。

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码


```js
hstRtcEngine.init()
.then(() => {
    console.log("Init success.");
})
.catch(() => {
    console.log("Init failed!");
})
```


## login

在使用平台提供的服务之前，需要先登录到平台，进行身份校验。


### 接口原型

```js
hstRtcEngine.login(options)
```

### 参数说明

options提供登录所需的参数，如下表所示：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| appId | string | 是 | 从后台管理系统获取 |
| token | string | 是 | 使用Token生成代码生成 |
| userId | string | 是 | 开发者自定义，请注意用户ID的定义约束 |


> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，后登录的会被拒绝。


### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

```js
hstRtcEngine.init()
.then(() => {
    console.log("Init success.");
})
.catch(() => {
    console.log("Init failed!");
})
```

### 示例代码


```js
let options = {
    appId: '7a02a8217cd541f990152ea666ee24bf',
    token: '001Sx04XAA406DvYyD8J3oEh/eSZFnogbLaFnwlXozD6QfHgzwvglCNrVj3wjjxldlRYRG28cGFdK9xgku3fhdMKY2pB3j1It4Omq8Quxx4xFH/2h3MbrWmsVCjh/N1cfsx',
    userId: 'user1'
};

hstRtcEngine.login(options)
.then(() => {
    console.log("Login success.");
})
.catch(() => {
    console.log("Login failed!");
})
```


## joinGroup

平台的很多服务是基于分组来提供的，只有加入分组后才能够使用这些服务和功能。


### 接口原型

```js
hstRtcEngine.joinGroup(groupId)
```

### 参数说明

groupId <string> 待加入的分组ID，分组ID由开发者自定义，请注意分组ID的定义约束。

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一分组ID的用户相当于在同一个会议房间中，可以在分组内广播和接收音视频、发送分组内消息等。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.joinGroup("test-group")
.then(() => {
    console.log("Join group success.");
})
.catch(() => {
    console.log("Join group failed!");
})
```

## leaveGroup

离开分组，将不再能使用基于分组的服务和功能。

调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 接口原型

```js
hstRtcEngine.leaveGroup()
```

### 参数说明

无参数，用户同一时刻只能加入一个分组中。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.leaveGroup()
.then(() => {
    console.log("Leave group success.");
})
.catch(() => {
    console.log("Leave group failed!");
})
```


## exit

退出分组，将不再能使用平台的所有服务和功能。

调用此接口后，如果在此之前没有调用离开分组接口，引擎内部会自动离开分组，相关行为定义请参考“离开分组”。

除此之外，在线和信令通道服务也将不能使用。


### 接口原型

```js
hstRtcEngine.exit()
```

### 参数说明

无参数。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

退出登录后，客户端将断开与平台的所有连接，由于网络问题，退出登录有可能收不到响应，因此，客户端可以不用等异步返回即可执行正常的清理工作。

### 示例代码

```js
hstRtcEngine.exit()
.then(() => {
    console.log("Exit success.");
})
.catch(() => {
    console.log("Exit failed!");
})

// do something cleanning without waiting for async callback
... 

```

## destroy

如果不再需要使用到RTC引擎，可以调用此接口销毁RTC引擎。

此接口内部会自动调用“离开分组”和“退出登录”。

### 接口原型

```js
hstRtcEngine.destroy()
```

### 参数说明

无参数。
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.destroy();
hstRtcEngine = null;
```

## on

用来订阅引擎通知事件。

### 接口原型

```js
hstRtcEngine.on(eventName, callback)
```

### 参数说明

eventName：需要订阅的事件名称，相关事件定义如下表所示。

| 事件名 | 回调参数 | 描述 |
| - | - | - |
|onGroupUserList | userId Array |服务器推送分组内所有用户列表，用户在加入分组后，会收到这个事件 |
|onUserJoinGroup | userId |有人加入分组 |
|onUserLeaveGroup | userId |有人离开分组 |
|onPublishMedia | {userId: "xxx", mediaType: "xxx", mediaId: "xxx"} |分组内有人发布媒体流 |
|onUnPublishMedia | {userId: "xxx", mediaType: "xxx", mediaId: "xxx"} |分组内有人取消发布媒体流 |
|onRemoteMediaAdd | {userId: "xxx", mediaType: "xxx", mediaId: "xxx", streamId: "xxx" }  |接收到远端媒体流 |
  
callback：事件发生时的回调函数，函数原型如下，不同事件data参数取值不一样。

```js
function callback(data)
```

> mediaType取值： 0-屏幕共享，1-音频，2-视频

### 返回值

无返回值。

### 示例代码

```js

hstRtcEngine.on('onGroupUserList', function(data){
    for (const user of data){
        console.log(user);
    }
});

hstRtcEngine.on('onUserJoinGroup', function(data){
    console.log(data + " join group.");
});

hstRtcEngine.on('onUserLeaveGroup', function(user){
    console.log(data + " leave group.");
}

hstRtcEngine.on('onPublishMedia', function (data) {
    hstRtcEngine.startReceiveRemoteVideo(data.userId, data.mediaId)
    .then(() => {
        console.log("Start receive user " + data.userId + " video.");
    })
    .catch(() => {
        console.log("Receive remote video failed!");
    })
}

hstRtcEngine.on('onUnPublishMedia', function (data) {
    hstRtcEngine.stopReceiveRemoteVideo(data.userId, data.mediaId)
    .then(() => {
        console.log("Stop receive remote video.");
    })
    .catch(() => {
        console.log("Stop receive remote video failed!");
    })
}

hstRtcEngine.on('onRemoteMediaAdd', function (data) {
     hstRtcEngine.setStreamRender(videoElement, data.streamId);
}
```

## startPublishVideo

开始广播本地视频。

### 接口原型

```js
hstRtcEngine.startPublishVideo(deviceId)
```

### 参数说明

deviceId： 为通过getMediaDevices枚举出来的摄像头设备deviceId。


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.startPublishVideo(deviceId);
```


## stopPublishVideo

停止广播本地摄像头设备。

### 接口原型

```js
hstRtcEngine.stopPublishVideo(deviceId)
```

### 参数说明

deviceId： 为通过getMediaDevices枚举出来的摄像头设备deviceId。

> 大多数情况下，stopPublishVideo与startPublishVideo成对调用，两者参数取值一致。  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.stopPublishVideo();
```


## setLocalVideoRender

设置本地视频渲染对象。

### 接口原型

```js
hstRtcEngine.setLocalVideoRender(videoElement, deviceId)
```

### 参数说明

videoElement： video标签对象。

deviceId： 设备标识，查询设备列表返回。
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
let videoElement = document.getElementById('test-video');
hstRtcEngine.setLocalVideoRender(videoElement, deviceId);
```

## unsetLocalVideoRender

取消设置本地视频渲染对象。

### 接口原型

```js
hstRtcEngine.unsetLocalVideoRender(videoElement, deviceId);
```

### 参数说明

videoElement： video标签对象。

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.unsetLocalVideoRender(videoElement);
```


## startReceiveRemoteVideo

开始接收远端视频。

### 接口原型

```js
hstRtcEngine.startReceiveRemoteVideo(userId, mediaId)
```

### 参数说明

userId： 用户ID，指定接收哪个用户的视频。

mediaId： 媒体ID，指定接收哪一路视频流。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.startReceiveRemoteVideo(userId, mediaId)
.then(() => {
    console.log("Start receive remote video.");
})
.catch(() => {
    console.log("Receive remote video failed!");
})
```


## stopReceiveRemoteVideo

停止接收远端视频。

### 接口原型

```js
hstRtcEngine.stopReceiveRemoteVideo(userId, mediaId)
```

### 参数说明

userId： 用户ID，指定接收哪个用户的视频。

mediaId： 媒体ID，指定接收哪一路视频流。

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.stopReceiveRemoteVideo(userId, mediaId)
.then(() => {
    console.log("Stop receive remote video!");
})
.catch(()=>{
    console.log("Stop receive remote video failed!");
})
```


## setStreamRender

设置远端视频渲染对象。

### 接口原型

```js
hstRtcEngine.setStreamRender(videoElement, streamId)
```

### 参数说明

videoElement： video标签对象。

streamId： 流标识，由订阅onRemoteMediaAdd事件返回。

> 音频、视频和屏幕共享都使用video标签进行播放。

> 一个Stream中可能同时包含音频和视频，onRemoteMediaAdd事件可能会通知两次，但只需调用setStreamRender一次即可。
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
let videoElement = document.getElementById('test-video');
hstRtcEngine.setStreamRender(videoElement, streamId);
```

## unsetStreamRender

取消设置远端视频渲染对象。

### 接口原型

```js
hstRtcEngine.unsetStreamRender(videoElement, streamId);
```

### 参数说明

videoElement： video标签对象。

streamId： 流标识，由订阅onRemoteMediaAdd事件返回。
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.unsetStreamRender(videoElement, streamId);
```


## getStats

获取音频流统计数据。

### 接口原型

```js
hstRtcEngine.getStats(options)
```

### 参数说明

options： 对流进行描述的参数对象，如下所示：

```js
{
    userId: "xxx", 
    mediaType: x,
    mediaId: "xxx"
}
```

> mediaType取值： 0-屏幕共享，1-音频，2-视频
  

### 返回值

返回统计数据对象，包含音频和视频统计数据，根据需要取对应统计值。

```js
{
    audio: { bitRate: xxx, totalBytes: xxx }
    video: { bitRate: xxx, totalBytes: xxx, frameRate: xxx, width: xxx, height: xxx }
}
```

> bitRate单位为kbps

### 示例代码

```js
// 使用定时器定时刷新统计数据
function displayVideoStats() {
    setTimeout(function() {
        let options = { userId: "xxx", mediaType: 2, mediaId: "xxxx" };
        let stats = hstRtcEngine.getStats(options);
        if (stats) {
            let statsInfo = stats.video.width + "*" 
                + stats.video.height + " " 
                + stats.video.frameRate + "fps " 
                + stats.video.bitRate + "kbps";
            console.log(statsInfo);
        } else {
            console.log("Get stats failed!");
        }
    displayVideoStats();
}
```


## getMediaDevices

获取摄像头设备。

### 接口原型

```js
hstRtcEngine.getMediaDevices()
```

### 参数说明

无参数。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象。

调用成功返回所有音频、视频设备列表，数据结构为：

```js
{
    micDev: [ { devName: "xxx", devId: "xxx" } ],
    spkDev: [ { devName: "xxx", devId: "xxx" } ],
    camDev: [ { devName: "xxx", devId: "xxx" } ]
}
```

调用失败返回错误。


### 示例代码

```js
hstRtcEngine.getMediaDevices()
.then((mediaDevs) => {
    // 麦克风设备
    for (const dev of mediaDevs.micDevs){
        console.log("MIC: " + dev.devName);
    }
    // 扬声器设备
    for (const dev of mediaDevs.spkDevs){
        console.log("SPK: " + dev.devName);
    }
    // 摄像头设备
    for (const dev of mediaDevs.camDevs){
        console.log("CAM: " + dev.devName);
    }
})
.catch(err => {
    console.log("Load media device failed!", err);
});
```