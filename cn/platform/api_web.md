## API列表
| 接口 | 描述 |
| - | - |
| init | 初始化RTC引擎 |
| login | 登录平台 |
| joinGroup | 加入分组 |
| leaveGroup | 离开分组 |
| logout | 登出平台 |
| destroy | 销毁引擎 |
| subEvent | 订阅事件 |
| unsubEvent | 取消订阅事件 |
| startPublishMedia | 开始广播本地媒体 |
| stopPublishMedia | 停止广播本地媒体 |
| startReceiveMedia | 开始接收远端媒体 |
| stopReceiveMedia | 停止接收远端媒体 |
| setMediaRender | 设置媒体播放对象 |
| unsetMediaRender | 取消设置媒体播放对象 |
| getStreamStats | 获取流统计数据 |
| getMediaDevices | 获取音频设备 |
| getOnlineUsers | 获取全量在线用户列表 |
| invite | 向在线用户发起邀请 |
| replyInvite | 响应在线邀请 |
| sendUserMsg | 发送在线消息 |
| sendGroupMsgWithWhiteList | 基于白名单发送分组消息 |
| sendGroupMsgWithBlackList | 基于黑名单发送分组消息 |
| sendGroupMsg | 发送分组内广播消息 |

## init

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```js
init()
```


### 参数说明

无

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码


```js
hstRtcEngine.init().then(() => {
    console.log("Init success.");
}).catch((err) => {
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

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 登录参数和选项 |

options成员如下所示：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| appId | string | 是 | 应用标识 |
| token | string | 是 | 鉴权信息 |
| companyId | string | 是 | 组织划分，可以用来控制在线状态的可见范围 |
| userId | string | 是 | 开发者自定义，请注意用户ID的定义约束 |
| mutexType | string | 否 | 标识同一用户的不同类型的登录 |
| forceLogin | boolean | 否 | 是否强制登录 |
| accessUrl | string | 否 | 服务器地址 |
| extendInfo | string | 否 | 自定义信息 |

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，如果forceLogin设置为false，则后登录的用户会被拒绝；如果forceLogin设置为true，则后登录的用户会挤掉前面登录的用户。

> accessUrl为null或者不填，则使用公有云服务；否则使用私有云服务。私有云服务该如何填写这个参数请参考部署文档或者咨询技术人员。

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码


```js
let options = {
    appId: '7a02a8217cd541f990152ea666ee24bf',
    token: '001Sx04XAA406DvYyD8J3oEh/eSZFnogbLaFnwlXozD6QfHgzwvglCNrVj3wjjxldlRYRG28cGFdK9xgku3fhdMKY2pB3j1It4Omq8Quxx4xFH/2h3MbrWmsVCjh/N1cfsx',
    companyId: "",
    userId: 'user1',
	mutextType: 'Web', 
    forceLogin: false,
	accessUrl: null,
    extendInfo: 'user-defined info'
};

hstRtcEngine.login(options).then(() => {
    console.log("Login success.");
}).catch(() => {
    console.log("Login failed!");
})
```


## joinGroup

平台的很多服务是基于分组提供的，只有加入分组后才能够使用这些服务和功能。


### 接口原型

```js
joinGroup(groupId)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | string | 是 | 待加入的分组ID，分组ID由开发者自定义，请注意分组ID的定义约束。 |

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 加入同一分组的用户相当于在同一个会议房间中，可以在分组内广播和接收音视频、发送分组内消息等。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.joinGroup("test-group").then(() => {
    console.log("Join group success.");
}).catch(() => {
    console.log("Join group failed!");
})
```

## leaveGroup

离开分组，将不再能使用基于分组的服务和功能。调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 接口原型

```js
leaveGroup()
```

### 参数说明

无参数

> 用户同一时刻只能加入到一个分组中。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.leaveGroup().then(() => {
    console.log("Leave group success.");
}).catch(() => {
    console.log("Leave group failed!");
})
```


## logout

退出登录，将不再能使用平台的所有服务和功能。


### 接口原型

```js
logout()
```

### 参数说明

无参数。
  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
hstRtcEngine.exit().then(() => {
    console.log("Exit success.");
}).catch(() => {
    console.log("Exit failed!");
})

```

## destroy

如果不再需要使用到RTC引擎，可以调用此接口销毁RTC引擎。

### 接口原型

```js
destroy()
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

## subEvent

订阅引擎通知事件。

### 接口原型

```js
subEvent(eventName, callback)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| eventName | string | 是 | 需要订阅的事件名称，相关事件定义如下表所示 |
| callback | function | 是 | 事件发生时的回调函数 |

支持订阅的事件类型定义如下表所示：

| 事件名 | 回调参数 | 描述 |
| - | - | - |
|onGroupUserList | userId Array |服务器推送分组内所有用户列表，用户在加入分组后，会收到这个事件 |
|onUserJoinGroup | userId |有人加入分组 |
|onUserLeaveGroup | userId |有人离开分组 |
|onPublishMedia | {userId: "xxx", mediaType: "xxx", mediaId: "xxx"} |分组内有人发布媒体流 |
|onUnPublishMedia | {userId: "xxx", mediaType: "xxx", mediaId: "xxx"} |分组内有人取消发布媒体流 |
|onRemoteMediaAdd | {userId: "xxx", mediaType: "xxx", mediaId: "xxx" }  | 接收到远端媒体流|
|onCommingInvite | {seqId: xxx, groupId: "xxx", userId: "xxx", userName: "xxx", extendInfo: "xxx"} | 收到别人邀请 |
|onInviteReply | {seqId: xxx, userId: "xxx", result: xxx} | 收到邀请响应 |
|onOnlineUserState | {userId: "xxx", mutexType: "xxx", customState: "xxx", extendInfo: "xxx" } | 在线用户实时上下线通知 |
|onRecvUserMsg | {srcUserId: "xxx", msg: "xxx", msgId: "xxx"} | 收到在线消息 |
|onRecvGroupMsg | {srcUserId: "xxx", msg: "xxx", msgId: "xxx", groupId: "xxx"} | 收到分组消息 |
  
callback原型如下所示：

```js
function callback(data)
```

### 返回值

无返回值。

### 示例代码

```js

hstRtcEngine.subEvent('onGroupUserList', function(data){
    for (const user of data){
        console.log(user);
    }
});

```

## unsubEvent

取消订阅引擎通知事件。

### 接口原型

```js
hstRtcEngine.unsubEvent([eventName])
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| eventName | string | 否 | 要取消订阅的事件名称，如果参数为空或为null，则表示取消已经订阅的所有事件 |

### 返回值

无返回值。

### 示例代码

```js
// 取消订阅'onGroupUserList'事件
hstRtcEngine.unsubEvent('onGroupUserList');

// 取消订阅所有事件
hstRtcEngine.unsubEvent();
```

## startPublishMedia

开始广播本地媒体，包括音频、视频、屏幕共享等。

### 接口原型

```js
startPublishMedia(mediaType, mediaId, options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| mediaId | string | 是 | 媒体ID，指定哪一路媒体 |
| options | object | 否 | 媒体选项，音频和屏幕共享暂不支持 |

options定义如下表所示：

| 成员 | 类型 | 描述 | 默认值 |
| - | - | - | - |
|width | number | 视频宽度 | 640 |
|height | number | 视频高度 | 480 |
|frameRate | number | 视频帧率 | 15 |
|bitRate | number | 视频码率 | 0 |

> bitRate单位为kbps，如果设置为0，则使用引擎内部默认码率。

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js

const MediaType = hstRtcEngine.MediaType;

// 广播音频
hstRtcEngine.startPublishMedia(MediaType.AUDIO, "microphone", null);

// 广播视频
let options = {
	width: 1920,
	height: 1080,
	frameRate: 25,
	bitRate: 0
}

// 广播屏幕共享
hstRtcEngine.startPublishMedia(MediaType.SCREEN_SHARE, null, null);

```


## stopPublishMedia

停止广播本地媒体，包括音频、视频和屏幕共享。

### 接口原型

```js
stopPublishMedia(mediaType, mediaId)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| mediaId | string | 是 | 媒体ID，指定哪一路媒体 |
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
const MediaType = hstRtcEngine.MediaType;

// 停止广播音频
hstRtcEngine.stopPublishMedia(MediaType.AUDIO);

// 停止广播视频
hstRtcEngine.stopPublishMedia(MediaType.VIDEO, "camera");

// 停止广播屏幕共享
hstRtcEngine.stopPublishMedia(MediaType.SCREEN_SHARE);

```


## startReceiveMedia

开始接收远端媒体，包括音频、视频、屏幕共享和电子白板。

### 接口原型

```js
startReceiveMedia(userId, mediaType, mediaId)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId | string | 是 | 用户ID，指定哪个用户 |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| mediaId | string | 是 | 媒体ID，指定哪一路媒体 |

  

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.startReceiveMedia(userId, MediaType.AUDIO, mediaId).then(() => {
    console.log("Start receive remote audio.");
}).catch(() => {
    console.log("Receive remote audio failed!");
})
```


## stopReceiveMedia

停止接收远端媒体，包括音频、视频、屏幕共享和电子白板。

### 接口原型

```js
stopReceiveMedia(userId, mediaType, mediaId)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId | string | 是 | 用户ID，指定哪个用户 |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| mediaId | string | 是 | 媒体ID，指定哪一路媒体 |

### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

### 示例代码

```js
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.stopReceiveMedia(userId, MediaType.AUDIO, mediaId)
.then(() => {
    console.log("Stop receive remote audio!");
})
.catch(()=>{
    console.log("Stop receive remote audio failed!");
})
```


## setMediaRender

设置媒体渲染对象。

### 接口原型

```js
setMediaRender(userId, mediaType, mediaId, renderElement, options)
```

### 参数说明

userId： 用户ID，指定停止接收哪个用户的媒体，如果是本地媒体，就填本地userId

mediaType： AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD

mediaId： 媒体ID，指定哪一路媒体

renderElement： 音频、视频和屏幕共享是video标签对象，电子白板是div标签对象

options： 如果是渲染本地视频和屏幕共享，则可以通过options指定渲染的分辨率、帧率，其它情况无效

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId | string | 是 | 用户ID，指定哪个用户 |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| mediaId | string | 是 | 媒体ID，指定哪一路媒体 |
| renderElement | object | 是 | 媒体渲染的标签对象，音频、视频和屏幕共享是video标签对象，电子白板是div标签对象 |
| options | object | 否 | 媒体选项，只有视频和屏幕共享支持 |

options成员变量定义如下：

| 成员 | 类型 | 描述 | 默认值 |
| - | - | - | - |
|width | number | 视频宽度 | 640 |
|height | number | 视频高度 | 480 |
|frameRate | number | 视频帧率 | 15 |

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
// 显示视频
const MediaType = hstRtcEngine.MediaType;

hstRtcEngine.setMediaRender(
	userId, 
	MediaType.VIDEO, 
	mediaId, 
	document.getElementById('test-video'));
```

## unsetMediaRender

删除媒体渲染对象。

### 接口原型

```js
unsetMediaRender(userId, mediaType, renderElement);
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId | string | 是 | 用户ID，指定哪个用户 |
| mediaType | number | 是 | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
| renderElement | object | 是 | 媒体渲染的标签对象，音频、视频和屏幕共享是video标签对象，电子白板是div标签对象 |
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
const MediaType = hstRtcEngine.MediaType;

// 取消显示视频
hstRtcEngine.unsetMediaRender(
	userId, 
	MediaType.VIDEO, 
	document.getElementById('test-video'));
```

## getStreamStats

获取流统计数据。

### 接口原型

```js
getStreamStats(options, callback, interval, userData)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 对流进行描述的参数对象 |
| callback | function | 是 | 回调函数 |
| interval | object | 是 | 回调时间间隔，单位毫秒 |
| userData | object | 否 | 自定义数据，回调callback时会传回来 |


options成员变量如下所示：

| 成员 | 类型 | 描述 |
| - | - | - |
|userId | string | 媒体所属用户 |
|mediaType | number | AUDIO/VIDEO/SCREEN_SHARE/WHITE_BOARD |
|mediaId | string  | 媒体ID，指定哪路媒体 |

callback函数原型如下：

```js
onGetStreamStats(stats, userData)
```

stats成员变量根据不同的媒体类型而变化，当媒体类型是音频时，stats只有一个成员变量volume，volume值小于1；当媒体类型是视频或屏幕共享时，stats的成员变量定义如下：

| 成员 | 类型 | 描述 |
| - | - | - |
|width | number | 视频宽度 |
|height | number | 视频高度 |
|frameRate | number  | 帧率 |
|bitRate | number  | 码流 |


### 返回值

无

### 示例代码

```js

// 显示视频统计数据
function displayVideoStats(userId, mediaId) {
    hstRtcEngine.getStreamStats({
        userId: userId,
        mediaType: MediaType.VIDEO,
        mediaId: mediaId
    }, function(stats, userData) {
        let videoInfo = stats.width + "*" + stats.height + " " +
                        stats.frameRate + "fps " +
                        stats.bitRate + "kbps "
        console.log(videoInfo);
    }, 1000, null)
}

// 显示音量
function displayAudioStats(userId, mediaId) {
    hstRtcEngine.getStreamStats({
        userId: userId,
        mediaType: MediaType.AUDIO,
        mediaId: mediaId
    }, function(stats, userData) {
		console.log(stats.volume)
    }, 100, userId)
}

```


## getMediaDevices

获取媒体设备。

### 接口原型

```js
getMediaDevices()
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


### 示例代码

```js
hstRtcEngine.getMediaDevices().then((mediaDevs) => {
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
}).catch(err => {
    console.log("Load media device failed!", err);
});
```

## getOnlineUsers

获取全量在线用户。

### 接口原型

```js
hstRtcEngine.getOnlineUsers()
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| callback | function | 是 | 回调函数 |

callback函数原型如下：

多页情况下会多次触发

```js
callback(pageData) // 格式如下
```

### 返回值

此方法如果没有填入callback回调函数，会返回一个Promise对象。（只会返回第一页数据 适合人数少的场景）

调用成功，会返回在线用于列表，数据结构如下所示：

```js
{
    pageInfo: { totalPages: 2, curPage: 1 },
    userInfo: [
        {
            userId: "xxx", 
            onlineInfo: [
                {
                    mutexType: "web",
                    customState: "xxx",
                    state: xxx
                }
                {
                    mutexType: "windows",
                    customState: "xxx",
                    state: xxx
                }
            ]
        }
        {
            userId: "xxx", 
            onlineInfo: [
                {
                    mutexType: "web",
                    customState: "xxx",
                    state: xxx
                }
                {
                    mutexType: "windows",
                    customState: "xxx",
                    state: xxx
                }
            ]
        }
    ]
}
```

> totalPages和curPage用来表示当前页码和总页数。

> mutexType用来实现同一用户在不同终端登录的情况。

> customState用来实现自定义在线状态。

### 示例代码

```js
// 带参数
hstRtcEngine.getOnlineUsers((data) => {
    for (const user of data.userInfo){
        console.log(user.userId);
    }
});
// 不带参数 不推荐
hstRtcEngine.getOnlineUsers()
.then (data => {
    for (const user of data.userInfo){
        console.log(user.userId);
    }
})
.catch(err => {
    console.log("Get online users failed!");
});
```


## invite

向在线用户发送邀请，至于邀请的内容以及邀请后的动作由开发者定义。

### 接口原型

```js
hstRtcEngine.invite(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 邀请参数和选项 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| seqId | number | 是 | 邀请序列号，用来区分不同的邀请 |
| groupId | string | 是 | 分组ID，邀请用户加入哪个分组 |
| calleeInfo | array | 是 | 邀请用户列表 |
| extendInfo | object | 否 | 自定义数据 |


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
let options = {
    seqId: 1,
    groupId: "test-group",
    calleeInfo: ["user1"],
    extendInfo: "instant call"
};
hstRtcEngine.invite(options);
```


## replyInvite

响应在线邀请。

### 接口原型

```js
hstRtcEngine.replyInvite(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 响应邀请参数和选项 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| seqId | number | 是 | 邀请序列号，用来区分不同的邀请 |
| groupId | string | 是 | 分组ID，邀请用户加入哪个分组 |
| operation | number | 是 | 0：接受邀请，1：拒绝邀请 |
| extendInfo | object | 否 | 自定义数据 |


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.on('onCommingInvite', function(data) {
    let result = confirm("是否接受来自分组ID为" + data.groupId + ", 用户ID为" + data.userId + "的邀请？");
    if (result) { // 接受邀请
        hstRtcEngine.replyInvite({seqId: data.seqId, groupId: data.groupId, operation: 0, extendInfo: ""});
    } else { // 拒绝邀请
        hstRtcEngine.replyInvite({seqId: data.seqId, groupId: data.groupId, operation: 1, extendInfo: ""});
    }
});
```

## sendUserMsg

发送在线消息。

> 在线消息只支持点对点发送。

### 接口原型

```js
hstRtcEngine.sendUserMsg(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 发送消息的参数 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| dstUserId | string | 是 | 消息发送的目标用户ID |
| msg | object | 是 | 消息内容 |


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.sendUserMsg({
	dstUserId: "userId1", 
	msg: "Hello"});
```


## sendGroupMsgWithWhiteList

基于白名单发送分组消息，当需要指定分组内某些人发送消息时，可以使用此接口。

### 接口原型

```js
hstRtcEngine.sendGroupMsgWithWhiteList(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 发送消息的参数 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | string | 是 | 发送消息的目标分组ID |
| whiteList | string | 是 | 白名单 |
| msg | object | 是 | 消息内容 |

> 白名单最大支持设置64个用户。


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
// 向分组内user1、user2、user3发送消息
let options = {
    groupId: "test-group",
    whiteList: ["user1", "user2", "user3"],
    msg: "Hello everybody!"
};
hstRtcEngine.sendGroupMsgWithWhiteList(options);
```


## sendGroupMsgWithBlackList

基于黑名单发送分组消息，当需要屏蔽分组内某些人发送消息时，可以使用此接口。

### 接口原型

```js
hstRtcEngine.sendGroupMsgWithBlackList(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 发送消息的参数 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | string | 是 | 发送消息的目标分组ID |
| blackList | string | 是 | 黑名单 |
| msg | object | 是 | 消息内容 |

> 黑名单最大支持设置64个用户。


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
// 向分组内除user1和user2之外的所有人发送消息
let options = {
    groupId: "test-group",
    whiteList: ["user1", "user2"],
    msg: "Hello everybody!"
};
hstRtcEngine.sendGroupMsgWithBlackList(options);
```


## sendGroupMsg

在分组内发送广播消息。

### 接口原型

```js
hstRtcEngine.sendGroupMsg(options)
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| options | object | 是 | 发送消息的参数 |

options成员变量定义如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | string | 是 | 消息发送的目标分组ID |
| msg | object | 是 | 消息内容 |


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
// 向分组内所有人发送消息
let options = {
    groupId: "test-group",
    msg: "Hello everybody!"
};
hstRtcEngine.sendGroupMsg(options);
```