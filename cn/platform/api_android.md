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
| startPreviewVideo | 本地视频增加预览渲染 |
| stopPreviewVideo | 本地视频删除预览渲染 |
| startPublishVideo | 开始广播视频 |
| stopPublishVideo | 停止广播视频 |
| switchCamera | 前后摄像头切换 |
| setAudioParam | 设置音频参数 |
| isFrontCamera | 当前是否用的前摄像头 |
| setVideoProfile | 设置本地视频profile, 如果设置的profile参数有不合理，SDK会做适当调整 |
| setRemoteVideoRender | 设置远端视频的渲染窗口 |
| getVideoStats | 获取视频的统计数据 |
| startPublishAudio | 开始广播音频 |
| stopPublishAudio | 停止广播音频 |
| getSpeakerEnergy | 获取扬声器能量 |
| getMicrophoneEnergy | 获取麦克风能量值 |
| getRemoteAudioEnergy | 获取远端用户的音频能量 |
| prepareScreenShare | 准备屏幕共享，会弹框选择。 activity 必现在 onActivityResult 里调用 startScreenShare |
| startScreenShare | 开始屏幕共享，必现在 onActivityResult 里调用 startScreenShare |
| stopScreenShare | 结束屏幕共享 |
| getFspBoard | 获取 IFspBoard  对象 |

## create

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```js
public static FspEngine create(Context context, String appid, FspEngineConfigure configure, IFspEngineEventHandler eventHandler)
```


### 参数说明
FspEngineContext 结构体说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| context |  Context | 是 | 全局context |
| app_id |  string | 是 | appid 由fsp平台分配的应用id |
| configure |  FspEngineConfigure | 否 | configure 配置，可以填null |
| event_handler | IFspEngineEventHandler * | 是 | 外部实现的事件回调对象 |

### 返回值

此方法会返回一个FspEngine对象。

### 示例代码

```js
FspEngineConfigure configure = new FspEngineConfigure();
        configure.serverAddr = serverAddr;
        configure.hardwareEncNumber = 1;
        configure.hardwareDecNumber = 0;
        configure.recvVoiceVariant = FspPreferenceManager.getInstance().getIsRecvVoiceVariant();

if (fspEngine == null) {
            fspEngine = 		FspEngine.create(MeetingDemoApplication.sApplication, appId, configure, this);
        }
```

## init

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```js
public abstract int init();
```


### 参数说明
无

### 返回值

此方法会返回一个int。

### 示例代码
```js
int value = fspEngine.init();
```
## getVersion

获取平台SDK版本，协助定位问题。


### 接口原型

```js
public abstract String getVersion();
```

### 参数说明

无

### 返回值

以字符串形式返回当前版本信息。

### 示例代码


```js
String strVersion = m_engine.GetVersion();
```

## login

在使用平台提供的服务之前，需要先登录到平台，进行身份校验。


### 接口原型

```js
public abstract int login(String token, String userId, boolean isForceLogin, String customInfo);
```

### 参数说明

options： 提供登录所需的参数，如下表所示：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| token | String | 是 | 鉴权信息 |
| userId | String | 是 | 应用标识 |
| isForceLogin | boolean | 否 | 是否强制登录 |
| customInfo | String | 否 | 自定义信息 |

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，如果forceLogin设置为false，则后登录的用户会被拒绝；如果forceLogin设置为true，则后登录的用户会挤掉前面登录的用户。


### 返回值

此方法会返回一个boolean对象。

### 示例代码


```js
boolean isForceLogin = FspPreferenceManager.getInstance().getIsForceLogin();

String token = FspToken.build(m_strAppid, m_strAppSecrectKey, userId);

boolean result = m_fspEngine.login(token, userId, isForceLogin, customName) == FspEngine.ERR_OK;
```

## loginOut

在退出平台提供的服务之前，需要先调用此接口，销毁资源。

### 接口原型

```js
public abstract int loginOut();
```

### 参数说明
无

### 返回值

此方法会返回一个int对象。

### 示例代码


```js
int ret = m_engine.loginOut()

```

## getFspSignaling

在退出平台提供的服务之前，需要先调用此接口，销毁资源。

### 接口原型

```js
public abstract IFspSignaling getFspSignaling();
```

### 参数说明
无

### 返回值

此方法会返回一个int对象。

### 示例代码


```js
 int errCode = m_fspEngine.getFspSignaling().refreshAllUserStatus();
```

## joinGroup

平台的很多服务是基于分组来提供的，只有加入分组后才能够使用这些服务和功能。


### 接口原型

```js
public abstract int joinGroup(String groupId);
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| groupId | String | 是 | 鉴权信息 |
groupId <string> 待加入的分组ID，分组ID由开发者自定义，请注意分组ID的定义约束。

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一分组ID的用户相当于在同一个会议房间中，可以在分组内广播和接收音视频、发送分组内消息等。


### 返回值

此方法会返回一个int对象。

### 示例代码

```js
String groupId
int err = m_engine.joinGroup(groupId)

```

## destroy

### 接口原型

```js
 public abstract void destroy();
```

### 参数说明

无参数，用户同一时刻只能加入一个分组中。


### 返回值

无

### 示例代码

```js
 m_engine.destroy();

```

## leaveGroup

离开分组，将不再能使用基于分组的服务和功能。

调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 接口原型

```js
public abstract int leaveGroup();
```

### 参数说明

无参数，用户同一时刻只能加入一个分组中。


### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.leaveGroup();

```

## startPreviewVideo

本地视频增加预览渲染


### 接口原型

```js
 public abstract int startPreviewVideo(SurfaceView renderView);
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| renderView |SurfaceView | 是 | 渲染句柄 |


### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.startPreviewVideo(previewRender);
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## stopPreviewVideo

本地视频增加预览渲染


### 接口原型

```js
public abstract int stopPreviewVideo();
```

### 参数说明
无

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.stopPreviewVideo();
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## startPublishVideo

本地视频增加预览渲染


### 接口原型

```js
public abstract int startPublishVideo();
```

### 参数说明
无

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.startPublishVideo();
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```
## stopPublishVideo

本地视频增加预览渲染


### 接口原型

```js
public abstract int stopPublishVideo();
```

### 参数说明
无

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.stopPublishVideo();
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## switchCamera

本地视频增加预览渲染


### 接口原型

```js
public abstract int switchCamera();
```

### 参数说明
无

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.switchCamera();
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## setAudioParam

本地视频增加预览渲染


### 接口原型

```js
public abstract int setAudioParam(int optionType, int optionValue);
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| optionType |int | 是 |optionType AUDIOPARAM的取值 |
| optionValue |int | 是 |optionValue 根据不同AUDIOPARAM 取值不同|

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.setAudioParam(optionType,optionValue);
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## isFrontCamera

本地视频增加预览渲染


### 接口原型

```js
public abstract int isFrontCamera();
```

### 参数说明
无

### 返回值
此方法返回一个int对象。

### 示例代码

```js
int fspErrCode = m_fspEngine.isFrontCamera();
if (fspErrCode != FspEngine.ERR_OK) {
	return false;
}
```

## setVideoProfile

设置本地视频profile, 如果设置的profile参数有不合理，SDK会做适当调整


### 接口原型

```js
 public abstract int setVideoProfile(VideoProfile profile);
```

### 参数说明

video_id 设置哪路视频的profile;profile profile参数;
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| video_id |const char* | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| profile |const VideoProfile& | 是 |视频参数描述 |

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
VideoProfile profile;
profile.width = 1280;		//视频宽
profile.height = 720;		 //视频高
profile.framerate = 15;		 //视频帧率
profile.recv_wnd_adapt = true;//是否自动适配接收端窗口，默认true
profile.net_bd_adapt     = true; //是否自动适应网络带宽调整视频参数, 默认true
int fspErrCode = m_engine.setVideoProfile(video_id,profile)
if (fspErrCode != fsp_core::ERR_OK) {
	return ;
}
```

## setRemoteVideoRender

设置远端用户视频的渲染窗口


### 接口原型

```js
public abstract int setRemoteVideoRender(String userId, String videoId, SurfaceView render_surface, int render_mode);
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |String | 是 |用户id |
| video_id |String | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| render_surface |SurfaceView| 是 |渲染窗口句柄 |
| render_mode |int| 是 |渲染模式选择（缩放、裁剪、平铺） |

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.setRemoteVideoRender(userId,videoId,render_surface,render_mode)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## getVideoStats

获取视频的统计数据, 一般定时调用获取。 支持获取远端和本端的统计，根据user_id区分


### 接口原型

```js
 public abstract VideoStatsInfo getVideoStats(String userId, String videoId);
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |String | 是 |用户id |
| video_id |String | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| stats |VideoStatsInfo| 是 |视频信息（宽、高、帧率、码率） |

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
VideoStatsInfo videoSatausinfo;
int err = m_engine.getVideoStats(user_id,video_id,&videoSatausinfo)
if (err != fsp_core::ERR_OK) {
	return ;
}
```


## startPublishAudio

开始广播音频


### 接口原型

```js
public abstract int startPublishAudio();
```

### 参数说明
无
### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.startPublishAudio(szAudioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## stopPublishAudio

停止广播音频


### 接口原型

```js
public abstract int stopPublishAudio();
```

### 参数说明

无

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int  err = m_engine.stopPublishAudio(szAudioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## getSpeakerEnergy

获取远端用户的音频能量


### 接口原型

```js
public abstract int getSpeakerEnergy();
```

### 参数说明
无

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.getSpeakerEnergy()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## getMicrophoneEnergy

获取远端用户的音频能量


### 接口原型

```js
public abstract int getMicrophoneEnergy();
```

### 参数说明
无

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.getMicrophoneEnergy()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## getRemoteAudioEnergy

获取远端用户的音频能量


### 接口原型

```js
public abstract int getRemoteAudioEnergy(String userId, String audioId);
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| userId |String | 是 |用户id |
| audioId |String | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |

### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.getRemoteAudioEnergy(userId,audioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```


## startScreenShare

开始屏幕共享, 如果已经在屏幕共享，可以继续调用更新共享参数


### 接口原型

```js
public abstract int startScreenShare(Activity activity, int responseCode, Intent data, Rect region);
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| activity |Activity| 活动avtivity |
| responseCode |int| 是 |共享区域的顶边y坐标; |
| data |Intent| 是 |组件 |
| region |Rect| 是 |共享区域的坐标; |
### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.startScreenShare( activity,  responseCode,  data,  region)；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## stopScreenShare

停止共享


### 接口原型

```js
public abstract int stopScreenShare();
```

### 参数说明
无
### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.stopScreenShare( )；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## getFspBoard

结束本地录制


### 接口原型

```js
public abstract IFspWhiteBoard getFspBoard();
```

### 参数说明
无
### 返回值

此方法会返回一个int对象。

### 示例代码

```js
int err = m_engine.getFspBoard()；
if (err != fsp_core::ERR_OK) {
	return ;
}

```