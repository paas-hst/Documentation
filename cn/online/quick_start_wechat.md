# 快速开始

本文演示如何快速使用在线相关接口，包括在线用户列表和邀请相关功能。

## 获取在线用户列表

登录成功后，应用应该立即调用getOnlineUsers接口获取全量在线用户列表，服务器只会主动推送增量用户上线和离线消息。

```js
hstRtcEngine.getOnlineUsers().then (data => {
    for (const user of data.userInfo){
        console.log(user.uid);
    }
}).catch(() => {
    console.log("Get online users failed!");
});
```

## 维护在线用户列表

当有用户上线/下线时，服务器会主动推送消息，开发者需要订阅“onOnlineUserState”事件，来侦听用户在线状态变化，并实时刷新本地在线用户列表。

```js
hstRtcEngine.subEvent('onOnlineUserState', function(data) {
    if (data.state == 1) { // 用户上线
        console.log("User " + data.userId + " online.");
    } else { // 用户下线
        console.log("User " + data.userId + " offline.");
    }
});
```

## 发送邀请

可以向在线用户发送邀请，邀请参数中携带groupId，用来实现在线呼叫功能。

```js
let inviteParam = {
    seqId: 1,             // 本地用来区分不同邀请请求
    groupId: groupId,     // 可以携带groupId
    calleeInfo: [userId], // 向谁发起邀请 
    extendInfo: ""        // 可以携带自定义参数
};
hstRtcEngine.invite(inviteParam);
```

## 回复邀请

收到其他人的邀请后，需要对邀请进行回复。开发者需要订阅“onCommingInvite”事件，监听其他人的在线邀请，收到邀请事件后，调用replyInvite回复邀请，可以接受或拒绝邀请。

```js
hstRtcEngine.subEvent('onCommingInvite', function(data) {
    let result = confirm("是否接受来自分组ID为" + param.groupId + ", 用户ID为" + param.userId + "的邀请？");
    if (result) { // 接受邀请
        hstRtcEngine.replyInvite({seqId: data.seqId, groupId: data.groupId, operation: 0, extendInfo: ""});
    } else { // 拒绝邀请
        hstRtcEngine.replyInvite({seqId: data.seqId, groupId: data.groupId, operation: 1, extendInfo: ""});
    }
});
```

## 邀请响应

在线邀请发出去以后，需要订阅“onInviteReply”事件来获取邀请响应。

```js
hstRtcEngine.subEvent('onInviteReply', function(data){
    if (data.result == 0) {
        console.log("用户 " + data.userId + " 接受了邀请!");
    } else {
        console.log("用户 " + data.userId + " 拒绝了邀请!");
    }
});
```