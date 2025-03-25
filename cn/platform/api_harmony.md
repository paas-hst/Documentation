## API列表
| 接口 | 描述 |
| - | - |
| create | 创建FspEngine实现 |
| init | 初始化RTC引擎 |
| getVersion | sdk版本信息 |
| login | 登录平台 |
| loginOut | 登出平台 |
| getFspSignaling | 获取业务信令IFspSignaling对象 |
| joinGroup | 加入分组 |
| leaveGroup | 离开分组 |
| destroy | 销毁引擎 |
| setLocalVideoRender | 设置本地视频的渲染窗口 |
| startPublishVideo | 开始广播视频 |
| stopPublishVideo | 停止广播视频 |
| setRemoteVideoRender | 设置远端视频的渲染窗口 |
| startPublishAudio | 开始广播音频 |
| stopPublishAudio | 停止广播音频 |
| getSpeakerEnergy | 获取扬声器能量 |
| getMicrophoneEnergy | 获取麦克风能量值 |
| getRemoteAudioEnergy | 获取远端用户的音频能量 |

## create

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```TYPESCRIPT
public static create() : FspEngine
```

### 参数说明
无

### 返回值

此方法会返回一个FspEngine对象。

### 示例代码

```TYPESCRIPT
if (fspEngine == null) {
    fspEngine = FspEngine.create();
}
```

## init

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```TYPESCRIPT
public abstract init(appId: string, serverAddr: string) : number;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| appId | string | 是 | appid 由fsp平台分配的应用id |
| serverAddr | string | 是 | 登录的服务器地址 |

### 返回值

此方法会返回一个number。

### 示例代码
```TYPESCRIPT
let res = fspEngine.init(appId, serverAddr);
```

## getVersion

获取平台SDK版本，协助定位问题。

### 接口原型

```TYPESCRIPT
public abstract getVersion() : string;
```

### 参数说明

无

### 返回值

以字符串形式返回当前版本信息。

### 示例代码


```TYPESCRIPT
let strVersion = fspEngine.getVersion();
```

## login

在使用平台提供的服务之前，需要先登录到平台，进行身份校验。


### 接口原型

```TYPESCRIPT
public abstract login(deviceId: string, token: string, userId: string, isForceLogin: boolean, customInfo: string) : number;
```

### 参数说明

options： 提供登录所需的参数，如下表所示：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| deviceId | string | 是 | 应用标识 |
| token | string | 是 | 鉴权信息 |
| userId | string | 是 | 用户标识 |
| isForceLogin | boolean | 否 | 是否强制登录 |
| customInfo | string | 否 | 自定义信息 |

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，如果forceLogin设置为false，则后登录的用户会被拒绝；如果forceLogin设置为true，则后登录的用户会挤掉前面登录的用户。


### 返回值

此方法会返回一个number值。

### 示例代码


```TYPESCRIPT
string token = fspToken.build(m_strAppid, m_strAppSecrectKey, userId);
let res = fspEngine.login(token, userId, isForceLogin, customName);
```

## loginOut

在退出平台提供的服务之前，需要先调用此接口，销毁资源。

### 接口原型

```TYPESCRIPT
public abstract loginOut() : number;
```

### 参数说明
无

### 返回值

此方法会返回一个number值。

### 示例代码


```TYPESCRIPT
let ret = fspEngine.loginOut();
```

## getFspSignaling

获取业务信令IFspSignaling对象。

### 接口原型

```TYPESCRIPT
public abstract getFspSignaling() : IFspSignaling;
```

### 参数说明
无

### 返回值

此方法会返回一个IFspSignaling对象。

### 示例代码


```TYPESCRIPT
 int errCode = fspEngine.getFspSignaling().refreshAllUserStatus();
```

## joinGroup

平台的很多服务是基于分组来提供的，只有加入分组后才能够使用这些服务和功能。


### 接口原型

```TYPESCRIPT
public abstract joinGroup(String groupId) : number;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | String | 是 | 鉴权信息 |
groupId <string> 待加入的分组ID，分组ID由开发者自定义，请注意分组ID的定义约束。

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一分组ID的用户相当于在同一个会议房间中，可以在分组内广播和接收音视频、发送分组内消息等。


### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
string groupId;
let err = fspEngine.joinGroup(groupId);

```

## destroy

销毁引擎

### 接口原型

```TYPESCRIPT
 public abstract destroy() : void;
```

### 参数说明

无参数。


### 返回值

无

### 示例代码

```TYPESCRIPT
fspEngine.destroy();
```

## leaveGroup

离开分组，将不再能使用基于分组的服务和功能。

调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 接口原型

```TYPESCRIPT
public abstract leaveGroup() : number;
```

### 参数说明

无参数。


### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let err = fspEngine.leaveGroup();

```

## setLocalVideoRender

设置本地视频的渲染窗口


### 接口原型

```TYPESCRIPT
 public abstract setLocalVideoRender(surfaceId: string) : number;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| surfaceId |string | 是 | surfaceView的id |


### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let fspErrCode = fspEngine.setLocalVideoRender("xc_localvideo");
```

> 停止渲染则指定null的surfaceId将不再渲染。


## startPublishVideo

开始广播视频


### 接口原型

```TYPESCRIPT
public abstract startPublishVideo(videoId: string) : number;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| videoId |string | 是 | 视频id |

### 返回值
此方法返回一个number值。

### 示例代码

```TYPESCRIPT
let fspErrCode = m_fspEngine.startPublishVideo('defaultCam');
```
## stopPublishVideo

停止广播视频


### 接口原型

```TYPESCRIPT
public abstract stopPublishVideo() : number;
```

### 参数说明
无

### 返回值
此方法返回一个number值。

### 示例代码

```TYPESCRIPT
let fspErrCode = m_fspEngine.stopPublishVideo();
```


## setRemoteVideoRender

设置远端用户视频的渲染窗口


### 接口原型

```TYPESCRIPT
public abstract setRemoteVideoRender(userId: string, videoId: string, surfaceId: string) : number;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId |string | 是 |用户id |
| videoId |string | 是 |视频id, 支持同时广播多路视频时，videoId标识每路视频; |
| surfaceId |string| 是 |surfaceView的id |

### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let err = fspEngine.setRemoteVideoRender(userId,videoId,"xc_remotevideo")
```


## startPublishAudio

开始广播音频


### 接口原型

```TYPESCRIPT
public abstract startPublishAudio() : number;
```

### 参数说明
无
### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let err = m_engine.startPublishAudio()
```

## stopPublishAudio

停止广播音频


### 接口原型

```TYPESCRIPT
public abstract stopPublishAudio() : number;
```

### 参数说明

无

### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let  err = m_engine.stopPublishAudio()
```

## getSpeakerEnergy

获取远端用户的音频能量


### 接口原型

```TYPESCRIPT
public abstract getSpeakerEnergy() : number;
```

### 参数说明
无

### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let value = fspEngine.getSpeakerEnergy()
```

## getMicrophoneEnergy

获取远端用户的音频能量


### 接口原型

```TYPESCRIPT
public abstract getMicrophoneEnergy() : number;
```

### 参数说明
无

### 返回值

此方法会返回一个number值。

### 示例代码

```TYPESCRIPT
let value = fspEngine.getMicrophoneEnergy()
```

## getRemoteAudioEnergy

获取远端用户的音频能量


### 接口原型

```TYPESCRIPT
public abstract getRemoteAudioEnergy(userId: string) : number;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId |string | 是 |用户id |

### 返回值

此方法会返回一个number。

### 示例代码

```TYPESCRIPT
let value = fspEngine.getRemoteAudioEnergy(userId)
```
