
## API列表
| 接口 | 描述 |
| - | - |
| on | 订阅事件 |
| sendUserMsg | 发送在线消息 |
| sendGroupMsgWithWhiteList | 基于白名单发送分组消息 |
| sendGroupMsgWithBlackList | 基于黑名单发送分组消息 |
| sendGroupMsg | 发送分组内广播消息 |


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
|onRecvUserMsg | {srcUserId: "xxx", msg: "xxx", msgId: "xxx"} | 收到在线消息 |
|onRecvGroupMsg | {srcUserId: "xxx", msg: "xxx", msgId: "xxx", groupId: "xxx"} | 收到分组消息 |
  
callback：事件发生时的回调函数，函数原型如下，不同事件data参数取值不一样。

```js
function callback(data)
```

### 返回值

无返回值

### 示例代码

```js
// 收到在线消息
hstRtcEngine.on("onRecvUserMsg", function(data) {
    console.log("Received online msg from " + data.srcUserId);
});

// 收到分组消息
hstRtcEngine.on("onRecvGroupMsg", function(data) {
    console.log("Received group msg from " + data.srcUserId);
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

options： 参数选项定义如下：

```js
{
    dstUserId: "xxx",
    msg: "xxxxxxxxxx"
}
```

> dstUserId： 消息发送的目标用户ID


### 返回值

此方法是一个同步调用，无返回值。

### 示例代码

```js
hstRtcEngine.sendUserMsg({dstUserId: "userId1", msg: "Hello"});
```


## sendGroupMsgWithWhiteList

基于白名单发送分组消息，当需要指定分组内某些人发送消息时，可以使用此接口。

### 接口原型

```js
hstRtcEngine.sendGroupMsgWithWhiteList(options)
```

### 参数说明

options： 参数选项定义如下：

```js
{
    groupId: xxx,
    whiteList: ["xxx", "xxx"],
    msg: "xxxxxxxxx"
}
```

> groupId: 消息发送的目标分组。

> whiteList： User ID列表，最多支持一次设置64个用户。


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

options： 参数选项定义如下：

```js
{
    groupId: xxx,
    blackList: ["xxx", "xxx"],
    msg: "xxxxxxxxx"
}
```

> groupId: 消息发送的目标分组。

> blackList： User ID列表，最多支持一次设置64个用户。


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

options： 参数选项定义如下：

```js
{
    groupId: xxx,
    msg: "xxxxxxxxx"
}
```

> groupId: 消息发送的目标分组。


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