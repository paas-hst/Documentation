# 快速开始

信令通道功能登录后即可使用，不过部分功能需要加入分组后才能使用，详见[加入组](../platform/prepare_web.md)。

## 发送在线消息

可以向在线用户发送消息，调用sendUserMsg接口实现，发送者只需要登录即可。

```js
hstRtcEngine.sendUserMsg({dstUserId: "HanMeimei", msg: "How are you!"});
```

## 发送分组消息

用户如果在分组中，可以发送分组消息。分组消息有三个接口，分别实现发送分组内广播、黑名单消息和白名单消息。其中黑名单消息和白名单消息用来实现分组内组播和点对点消息（私聊）。

```js
// 分组内广播消息
hstRtcEngine.sendGroupMsg({msg: sendText, groupId: window.groupId});

// 基于黑名单的分组内组播，发送给分组内除“HanMeimei”外所有人
hstRtcEngine.sendGroupMsgWithBlackList({
    msg: "Hello",
    groupId: "group1",
    blackList: ["HanMeimei"]
});

// 基于白名单的分组内组播，发送给分组内的“HanMeimei”和“Lilei”
hstRtcEngine.sendGroupMsgWithBlackList({
    msg: "Hello",
    groupId: "group1",
    whiteList: ["HanMeimei", "Lilei"]
});

// 基于白名单的点对点消息，给“HanMeimei”发私聊消息
hstRtcEngine.sendGroupMsgWithBlackList({
    msg: "Hello",
    groupId: "group1",
    whiteList: ["HanMeimei"]
});
```

> 发送分组消息，接收端无法区分消息是广播消息还是私聊消息，如果想区分这两种消息，私聊消息请用“发送在线消息”的接口。

## 接收在线消息

需要订阅“onRecvUserMsg”事件。

```js
hstRtcEngine.on("onRecvUserMsg", function(data) {
    console.log("Received online msg: " + data.msg + " from " + data.srcUserId );
});
```

## 接收分组消息

用户加入分组后，订阅“onRecvGroupMsg”事件即可接收到分组内的所有消息。

```js
hstRtcEngine.on("onRecvGroupMsg", function(data) {
    console.log("Received group msg: " + data.msg + " from " + data.srcUserId );
});
```