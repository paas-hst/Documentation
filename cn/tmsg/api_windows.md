## API列表
| 接口 | 描述 |
| - | - |
| Init | 初始化RTC引擎 |
| GetVersion | sdk版本信息 |
| Login | 登录平台 |
| Logout | 登出平台 |
| GetFspSignaling | 获取业务信令IFspSignaling对象 |
| JoinGroup | 加入分组 |
| LeaveGroup | 离开分组 |
| Destroy | 销毁引擎 |
| AddVideoPreview | 本地视频增加预览渲染 |
| RemoveVideoPreview | 本地视频删除预览渲染 |
| StartPublishVideo | 开始广播视频 |
| StopPublishVideo | 停止广播视频 |
| SetVideoProfile | 设置本地视频profile |
| SetRemoteVideoRender | 设置远端视频的渲染窗口 |
| GetVideoStats | 获取视频的统计数据 |
| RegisterLocalVideoFrameObserver | 注册本地视频观测器对象 |
| RegisterRemoteVideoFrameObserver | 注册远端视频观测器对象 |
| RegisterAudioFrameObserver | 注册语音观测器对象 |
| StartPublishAudio | 开始广播音频 |
| StopPublishAudio | 停止广播音频 |
| StartPlayAudio | 开始播放音频(全局) |
| StopPlayAudio | 停止播放音频（全局） |
| GetRemoteAudioEnergy | 获取远端用户的音频能量 |
| MuteRemoteAudio | 开关远端音频 |
| GetDeviceManager | 获取engine 的IDeviceManager |
| GetAudioEngine | 获取engine的 IAudioEngine |
| StartPublishScreenShare | 开始屏幕共享 |
| StopPublishScreenShare | 停止共享 |
| StartRecord | 开始本地录制 |
| StopRecord | 结束本地录制 |
| RemoteControlOperation | 远程控制操作 |


## Init

创建RTC引擎后，需要立即进行初始化，初始化成功后才能够调用其他接口和使用引擎提供的功能。

### 接口原型

```js
virtual ErrCode Init(const FspEngineContext &context) = 0;
```


### 参数说明
FspEngineContext 结构体说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| event_handler | IFspEngineEventHandler * | 是 | 外部实现的事件回调对象 |
| app_id |  string | 是 | appid 由fsp平台分配的应用id |
| log_path | string | 否 | 日志目录，如果不填，默认程序所在目录 |
| plugin_cfg_path | string | 是 | 插件管理配置文件目录，如果不填，默认为AVPlugins |
| auto_open_remote_audio | bool | 是 | 是否自动接听远端音频|
| recv_voice_variant | int | 是 | 接收变声选项|

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码


```js
fsp::FspEngineContext context;
context.event_handler 	= this;
context.log_path 		= "";
context.app_id 			= appid.c_str();
context.server_addr 	= serveraddr.c_str();
fsp::ErrCode err 		= m_engine->Init(context);
if (err != fsp_core::ERR_OK) {
	return ;
}
```
## GetVersion

获取平台SDK版本，协助定位问题。


### 接口原型

```js
virtual String GetVersion() = 0;
```

### 参数说明

无

### 返回值

以字符串形式返回当前版本信息。

### 示例代码


```js
std::string strVersion = m_engine->GetVersion();
```

## Login

在使用平台提供的服务之前，需要先登录到平台，进行身份校验。


### 接口原型

```js
virtual ErrCode Login(const char* fsp_token, const char* user_id, bool is_force_login, const char* custom_info) = 0;
```

### 参数说明

options： 提供登录所需的参数，如下表所示：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| fsp_token | const char * | 是 | 鉴权信息 |
| user_id |  const char * | 是 | 应用标识 |
| is_force_login | bool | 否 | 是否强制登录 |
| custom_info | const char * | 否 | 自定义信息 |

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一App下相同的User ID，如果forceLogin设置为false，则后登录的用户会被拒绝；如果forceLogin设置为true，则后登录的用户会挤掉前面登录的用户。


### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码


```js
fsp::ErrCode err = m_engine->Login(fsp_token, user_id, is_force_login, custom_info)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## Logout

在退出平台提供的服务之前，需要先调用此接口，销毁资源。

### 接口原型

```js
virtual ErrCode Logout() = 0;
```

### 参数说明
无

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码


```js
fsp::ErrCode err = m_engine->Logout()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## GetFspSignaling

在退出平台提供的服务之前，需要先调用此接口，销毁资源。

### 接口原型

```js
virtual IFspSignaling* GetFspSignaling() = 0;
```

### 参数说明
无

### 返回值

此方法会返回一个IFspSignaling指针对象。

### 示例代码


```js
IFspSignaling pFspSignaling = m_engine->GetFspSignaling()
if (nullptr != pFspSignaling) {
	return ;
}
```

## JoinGroup

平台的很多服务是基于分组来提供的，只有加入分组后才能够使用这些服务和功能。


### 接口原型

```js
virtual ErrCode JoinGroup(const char* group_id) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| group_id | const char * | 是 | 鉴权信息 |
groupId <string> 待加入的分组ID，分组ID由开发者自定义，请注意分组ID的定义约束。

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

> 同一分组ID的用户相当于在同一个会议房间中，可以在分组内广播和接收音视频、发送分组内消息等。


### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->JoinGroup(group_id)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## LeaveGroup

离开分组，将不再能使用基于分组的服务和功能。

调用此接口后，引擎内部会自动停止和关闭与分组相关的服务：

- 会关闭所有正在广播的音频、视频和屏幕共享。

- 会停止接收所有的音频、视频和屏幕共享。

- 不再会接收到分组内的事件通知。


### 接口原型

```js
virtual ErrCode LeaveGroup() = 0;
```

### 参数说明

无参数，用户同一时刻只能加入一个分组中。


### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->LeaveGroup()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## AddVideoPreview

本地视频增加预览渲染


### 接口原型

```js
virtual ErrCode AddVideoPreview(int camera_id, HWND render_wnd, RenderMode mode) = 0;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| camera_id |int | 是 | 相机index |
| render_wnd |  HWND | 是 | 渲染句柄 |
| mode | RenderMode | 是 | 渲染模式选择 |


### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->AddVideoPreview( camera_id,  render_wnd,  mode)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## StopPublishVideo

本地视频增加预览渲染


### 接口原型

```js
virtual ErrCode StopPublishVideo(const char* video_id) = 0;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| video_id |const char* | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StopPublishVideo(video_id)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## SetVideoProfile

设置本地视频profile, 如果设置的profile参数有不合理，SDK会做适当调整


### 接口原型

```js
virtual ErrCode SetVideoProfile(const char* video_id, const VideoProfile& profile) = 0;
```

### 参数说明

video_id 设置哪路视频的profile;profile profile参数;
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| video_id |const char* | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| profile |const VideoProfile& | 是 |视频参数描述 |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
VideoProfile profile;
profile.width = 1280;		//视频宽
profile.height = 720;		 //视频高
profile.framerate = 15;		 //视频帧率
profile.recv_wnd_adapt = true;//是否自动适配接收端窗口，默认true
profile.net_bd_adapt     = true; //是否自动适应网络带宽调整视频参数, 默认true
fsp::ErrCode err = m_engine->SetVideoProfile(video_id,profile)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## SetRemoteVideoRender

设置远端用户视频的渲染窗口


### 接口原型

```js
virtual ErrCode SetRemoteVideoRender(const char* user_id,
	  const char* video_id,
	  HWND render_wnd,
	  RenderMode mode) = 0;
```

### 参数说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |const char* | 是 |用户id |
| video_id |const char* | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| render_wnd |HWND| 是 |渲染窗口句柄 |
| mode |RenderMode| 是 |渲染模式选择（缩放、裁剪、平铺） |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->SetRemoteVideoRender(user_id,video_id,render_wnd,mode)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## GetVideoStats

获取视频的统计数据, 一般定时调用获取。 支持获取远端和本端的统计，根据user_id区分


### 接口原型

```js
 virtual ErrCode GetVideoStats(const char* user_id, const char* video_id,
	  VideoStatsInfo *stats) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |const char* | 是 |用户id |
| video_id |const char* | 是 |视频id, 支持同时广播多路视频时，video_id标识每路视频; |
| stats |VideoStatsInfo| 是 |视频信息（宽、高、帧率、码率） |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
VideoStatsInfo videoSatausinfo;
fsp::ErrCode err = m_engine->GetVideoStats(user_id,video_id,&videoSatausinfo)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## RegisterLocalVideoFrameObserver

注册本地视频观测器对象，即注册回调，当需要引擎给出 onCaptureVideoFrame 或 onRenderVideoFrame 回调时


### 接口原型

```js
 virtual ErrCode RegisterLocalVideoFrameObserver(int camera_id, IVideoFrameObserver *observer) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| camera_id |int | 是 |相机id |
| observer |IVideoFrameObserver| 是 |视频帧观察者 |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
IVideoFrameObserver *pVideoFrameObserver = new VideoFrameObserverImpl();
fsp::ErrCode err = m_engine>RegisterLocalVideoFrameObserver(camera_id,pVideoFrameObserver)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## RegisterRemoteVideoFrameObserver

注册远端视频观测器对象，即注册回调，当需要引擎给出 onCaptureVideoFrame 或 onRenderVideoFrame 回调时


### 接口原型

```js
 virtual ErrCode RegisterRemoteVideoFrameObserve(const char* user_id, const char* video_id, IVideoFrameObserver *observer) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |const char* | 是 |用户id |
| video_id |const char* | 是 |流id |
| observer |IVideoFrameObserver| 是 |视频帧观察者 |


### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
IVideoFrameObserver *pVideoFrameObserver = new VideoFrameObserverImpl();
fsp::ErrCode err = m_engine->RegisterLocalVideoFrameObserver(user_id，camera_id,pVideoFrameObserver)
if (err != fsp_core::ERR_OK) {
	return ;
}
```


## RegisterAudioFrameObserver

注册语音观测器对象，即注册回调，当需要引擎给出 onRecordAudioFrame 或 onPlaybackAudioFrame 回调时


### 接口原型

```js
 virtual ErrCode RegisterAudioFrameObserver(IAudioFrameObserver *observer) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| observer |IVideoFrameObserver| 是 |视频帧观察者 |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
IAudioFrameObserver *pAudioFrameObserver = new AudioFrameObserverImpl();
fsp::ErrCode err = m_engine->RegisterAudioFrameObserver(pAudioFrameObserver)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## StartPublishAudio

开始广播音频


### 接口原型

```js
 virtual ErrCode StartPublishAudio(const char* szAudioId) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| szAudioId |const char*| 是 |音频流id，必须取值 fsp::RESERVED_AUDIOID_MICROPHONE 或 fsp::RESERVED_AUDIOID_DESKTOP |
### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StartPublishAudio(szAudioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## StopPublishAudio

停止广播音频


### 接口原型

```js
 virtual ErrCode StopPublishAudio(const char* szAudioId) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| szAudioId |const char*| 是 |音频流id，必须取值 fsp::RESERVED_AUDIOID_MICROPHONE 或 fsp::RESERVED_AUDIOID_DESKTOP |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StopPublishAudio(szAudioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## StartPlayAudio

开始播放音频，如果在FspEngineContext中设置了自动播放音频，则不需要手动调用此接口


### 接口原型

```js
virtual ErrCode StartPlayAudio() = 0;
```

### 参数说明
无

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StartPlayAudio()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## StopPlayAudio

停止播放音频


### 接口原型

```js
virtual ErrCode StopPlayAudio() = 0;
```

### 参数说明
无

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StopPlayAudio()
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## GetRemoteAudioEnergy

获取远端用户的音频能量


### 接口原型

```js
virtual int GetRemoteAudioEnergy(const char* szUserId, const char* szAudioId) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| szUserId |const char*| 是 |对应的远端用户id |
| szAudioId |const char*| 是 |szAudioId 音频id, 必须取值 fsp::RESERVED_AUDIOID_MICROPHONE 或 fsp::RESERVED_AUDIOID_DESKTOP |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->GetRemoteAudioEnergy(szUserId，szAudioId)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## MuteRemoteAudio

开关远端音频


### 接口原型

```js
virtual ErrCode MuteRemoteAudio(const char* szUserId, const char* szAudioId, bool is_mute) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| szUserId |const char*| 是 |对应的远端用户id |
| szAudioId |const char*| 是 |szAudioId 音频id, 必须取值 fsp::RESERVED_AUDIOID_MICROPHONE 或 fsp::RESERVED_AUDIOID_DESKTOP |
| is_mute |bool| 是 |is_mute true关闭远端音频，false打开； |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->MuteRemoteAudio(szUserId，szAudioId，is_mute)
if (err != fsp_core::ERR_OK) {
	return ;
}
```

## GetDeviceManager

获取engine 的IDeviceManager


### 接口原型

```js
virtual IDeviceManager *GetDeviceManager() = 0;
```

### 参数说明
无
### 返回值

此方法会返回一个IDeviceManager指针对象。

### 示例代码

```js
IDeviceManager *pDeviceManager = m_engine->GetDeviceManager()
if (nullptr != pDeviceManager) {
	return ;
}
```

## GetAudioEngine

获取engine的 IAudioEngine


### 接口原型

```js
virtual IAudioEngine *GetAudioEngine() = 0;
```

### 参数说明
无
### 返回值

此方法会返回一个IDeviceManager指针对象。

### 示例代码

```js
IAudioEngine *pAudioEngine = m_engine->GetAudioEngine()
if (nullptr != pAudioEngine) {
	return ;
}
```

## StartPublishScreenShare

开始屏幕共享, 如果已经在屏幕共享，可以继续调用更新共享参数


### 接口原型

```js
virtual ErrCode StartPublishScreenShare(int left, int top, int right, int bottom, ScreenShareQualityBias quality_bias) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| left |int| 是 |共享区域的左边x坐标; |
| top |int| 是 |共享区域的顶边y坐标; |
| right |int| 是 |共享区域的右边x坐标; |
| bottom |int| 是 |共享区域的底边y坐标; |
| quality_bias |ScreenShareQualityBias| 是 |共享的质量偏好模式; |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StartPublishScreenShare( left,  top,  right,  bottom, ScreenShareQualityBias::quality_bias)；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## StopPublishScreenShare

停止共享


### 接口原型

```js
virtual ErrCode StopPublishScreenShare() = 0;
```

### 参数说明
无
### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StopPublishScreenShare( )；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## StartRecord

开始本地录制


### 接口原型

```js
 virtual ErrCode StartRecord(const char* file_path, int left, int top, int width, int height, bool is_record_audio) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| file_path |const char* | 是 |录制文件的全路径,包含文件后缀.mp4，比如d:/yourname.mp4；|
| left |int| 是 |共享区域的左边x坐标; |
| top |int| 是 |共享区域的顶边y坐标; |
| width |int| 是 |录制屏幕宽; |
| height |int| 是 |录制屏幕高; |
| is_record_audio |bool| 是 |是否录制音频; |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StartRecord(file_path,  left,  top,  width,  height,  is_record_audio )；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## StopRecord

结束本地录制


### 接口原型

```js
virtual ErrCode StopRecord() = 0;
```

### 参数说明
无
### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->StopRecord()；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## RemoteControlOperation

结束本地录制


### 接口原型

```js
virtual ErrCode RemoteControlOperation(const char* user_id, RemoteControlOperationType operation_type) = 0;
```

### 参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id |const char* | 是 | 对方userid|
| operation_type |RemoteControlOperationType| 是 |操作类型 |

### 返回值

此方法会返回一个fsp_core::ErrCode枚举对象。

### 示例代码

```js
fsp::ErrCode err = m_engine->RemoteControlOperation(user_id，operation_type)；
if (err != fsp_core::ERR_OK) {
	return ;
}

```

## GetFspWhiteBoard

结束本地录制


### 接口原型

```js
virtual IFspWhiteBoard* GetFspWhiteBoard() = 0;
```

### 参数说明
无
### 返回值

此方法会返回一个IFspWhiteBoard枚举对象。

### 示例代码

```js
IFspWhiteBoard *pFspWhiteBoard = new FspWhiteBoardImpl()
pFspWhiteBoard = m_engine->GetFspWhiteBoard()；
if (nullptr != pFspWhiteBoard) {
	return ;
}

```



