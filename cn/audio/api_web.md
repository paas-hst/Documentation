
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
| startPublishAudio | 广播本地音频 |
| stopPublishAudio | 停止广播本地音频 |
| startReceiveRemoteAudio | 接收远端音频 |
| stopReceiveRemoteAudio | 停止接收远端音频 |
| setStreamRender | 设置音频播放对象 |
| unsetStreamRender | 取消设置音频播放对象 |
| getStats | 获取音频流统计数据 |
| getMediaDevices | 获取音频设备 |
| chooseMicDevice | 选择本地麦克风设备 |

## 初始化

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 方法原型


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


## 登录

在使用平台提供的服务之前，需要先登录到平台，进行身份校验。


### 方法原型

```js
hstRtcEngine.login(options)
```

### 参数说明

options <object> 提供登录所需的参数，如下表所示：

| 参数名 | 类型 | 是否必填 | 参数说明
| :-: | :-: | :-: | - |
| appId | string | 是 | 从后台管理系统获取 |
| token | string | 是 | 使用Token生成代码生成 |
| userId | string | 是 | 开发者自定义，请注意用户ID的定义约束 |

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，后登录的会被拒绝。


### 返回值

此方法是一个异步调用，会返回一个Promise对象，异步调用结果没有参数。

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


```js
hstRtcEngine.login(options)
```


## 加入分组

平台的很多服务是基于分组来提供的，只有加入分组后才能够使用这些服务和功能。


### 方法原型

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

## 离开分组

离开分组，将不再能使用基于分组的服务和功能。

调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 方法原型

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


## 退出登录

退出分组，将不再能使用平台的所有服务和功能。

调用此接口后，如果在此之前没有调用离开分组接口，引擎内部会自动离开分组，相关行为定义请参考“离开分组”。

除此之外，在线和信令通道服务也将不能使用。


### 方法原型

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

## 销毁引擎

如果不再需要使用到RTC引擎，可以调用此接口销毁RTC引擎。

此接口内部会自动调用“离开分组”和“退出登录”。

### 方法原型

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

## 订阅事件

用来获取引擎的事件通知。

### 方法原型

```js
hstRtcEngine.on(eventName, callback)
```

### 参数说明

eventName：需要订阅的事件名称，相关事件定义如下表所示。

| 事件名 | 描述 |
| - | - |
|onGroupUserList | 服务器推送分组内所有用户列表，用户在加入分组后，会收到这个事件 |
|onUserJoinGroup | 有人加入分组 |
|onUserLeaveGroup | 有人离开分组 |
|onPublishMedia | 分组内有人发布音频，根据mediaType判断是否是音频 |
|onUnPublishMedia | 分组内有人取消发布音频，根据mediaType判断是否是音频 |
|onRemoteMediaAdd | 接收到远端音频流, 根据mediaType判断是否是音频 |
  

### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.destroy();
hstRtcEngine = null;
```

