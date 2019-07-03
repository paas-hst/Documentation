# 快速开始

透明消息功能需要加入组才能使用，详见[加入组](../platform/prepare_android.md)。

## 初始化

透明消息都通过 IFspSignaling 接口来调用，初始时需要向IFspSignaling注册回调实现对象。

```java
IFspSignaling fspSignaling = m_fspEngine.getFspSignaling();
fspSignaling.addEventHandler(this);
```

> 在线和透明消息都通过 IFspSignaling 接口调用，只需初始化一次。

## 发送消息

IFspSignaling 提供4个消息发送的方法，分别对应不同的接收者:

1. sendUserMsg 发给指定的单个用户，对方需要不再组内。
2. sendGroupMsg 发给组内所有用户
3. sendWhiteListGroupMsg 白名单方式发给组内部分用户，组内白名单列表可以收到
4. sendBlackListGroupMsg 黑名单方式发给组内部分用户，黑名单列表外的所有组内用户会收到

消息发送后，接收方会收到对应回调。

## 接收消息

初始化时注册回调后，有消息收到会通过相应回调通知。

1. onUserMsgIncome 会收到 sendUserMsg 发送的消息。
2. onGroupMsgIncome 会收到 sendGroupMsg、sendWhiteListGroupMsg、sendBlackListGroupMsg发送的消息。

