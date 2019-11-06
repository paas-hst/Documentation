
## API列表
| 接口 | 描述 |
| - | - |
| on | 订阅事件 |
| getOnlineUsers | 获取全量在线用户列表 |
| invite | 向在线用户发起邀请 |
| replyInvite | 响应在线邀请 |


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
|onCommingInvite | {seqId: xxx, groupId: "xxx", userId: "xxx", userName: "xxx", extendInfo: "xxx"} | 收到别人邀请 |
|onInviteReply | {seqId: xxx, userId: "xxx", result: xxx} | 收到邀请响应 |
  
callback：事件发生时的回调函数，函数原型如下，不同事件data参数取值不一样。

```js
function callback(data)
```

### 返回值

无返回值。

### 示例代码

```js
// 收到邀请
hstRtcEngine.on('onCommingInvite', function(data){
    console.log("User " + data.userId + " invite you to join group " +data.groupId);
    // 回复接受邀请
    hstRtcEngine.replyInvite(data.reqId, data.groupId, 1, "");
});

// 收到邀请响应
hstRtcEngine.on('onInviteReply', function(data){
    if (data.result == 0) {
    }    
    console.log(" join group.");
});

hstRtcEngine.on('onUserLeaveGroup', function(user){
    console.log(data + " leave group.");
}
```

## getOnlineUsers

获取全量在线用户。

### 接口原型

```js
hstRtcEngine.getOnlineUsers()
```

### 参数说明

无参数


### 返回值

此方法是一个异步调用，会返回一个Promise对象。

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

> totalPages和curPage用来实现分页拉取，当在线用户比较多时会用到。

> mutexType用来实现同一用户在不同终端登录的情况。

> customState用来实现自定义在线状态。

### 示例代码

```js
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

options： 邀请参数选项，数据结构定义如下：

```js
{
    seqId: xxx,
    groupId: "xxx",
    calleeInfo: ["xxx", "xxx"],
    extendInfo: "xxxxxxxxx"
}
```

> seqId： 用来标识是哪一个邀请，便于与邀请响应进行匹配。

> groupId: 协助实现邀请加入分组，类似于微信的呼叫音视频通话的功能。

> calleeInfo： User ID列表，支持同时呼叫多个用户。

> extendInfo： 开发者自定义数据。


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

options： 参数对象，定义如下：

```js
{
    seqId: xxx,
    groupId: "xxx",
    operation: x,
    extendInfo: "xxx"
}
```

> seqId： 必须填邀请请求中的seqId。

> groupId： 必须填邀请请求中的groupId。

> operation： 0-接受邀请，1-拒绝邀请

> extenInfo： 开发者自定义。


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