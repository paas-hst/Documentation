# 快速开始

音频通信需要登录后并成功加入组，详见[加入组](../platform/prepare_web.md)。

## 广播音频

unmute()广播本地音频：

```js
$hstEngine.unmute()
```

此接口没有返回值

音频广播后，组内所有用户会收到音频广播事件。

## 停止接听远端音频

mute()停止广播本地音频：

```js
$hstEngine.mute()
```

此接口没有返回值