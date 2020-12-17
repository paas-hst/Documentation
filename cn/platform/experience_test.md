# 体验试用

您可以通过平台提供的DEMO快速体验好视通云通信平台提供的各种产品和服务。

## 准备工作

请[点此](demo)获取各平台和产品对应的DEMO，其中Windows和macOS需要下载到本地运行，Android、iOS和微信小程序扫码体验，Web、云录制、云直播可以在线体验。

## MeetingDemo

MeetingDemo是基于各终端SDK开发的DEMO，用来演示终端功能和特性，可以在对应终端上进行体验。体验MeetingDemo总共可以分为以下几步，下面以Windows系统上CPP开发的DEMO进行演示。

### 1. 配置

MeetingDemo需要配置App ID、App Secret才可以运行。为了方便开发者快速体验，DEMO中内置了默认的App ID、App Secret，因此，如果想快速体验，无需任何配置即可运行。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/meeting-demo-1.png" align="center" />

> 默认App配置只用来快速体验，不可用作生产配置。

> 所有终端平台DEMO，都支持自有App配置。

> 如果需要测试私有云，则还需要配置私有云服务器地址，具体请咨询技术人员。

### 2. 登录平台

登录平台需要User ID，User ID是自定义的，不需要提前创建用户或者同步账号，但User ID的定义需要满足一定的规则，如下所示。另外，还需要保证在User ID在App中是唯一的，如果已经有相同User ID的用户登录平台，则后登录的用户会被拒绝，当然，你可以使用强制登录选项，将前面的用户踢掉。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/meeting-demo-2.png" align="center" />

> User ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

登录平台后，就可以看到相同APP下的在线用户列表。

### 3. 加入分组

如果要体验互动，则需要多人加入同一个分组，分组用Group ID标识，和User ID一样，Group ID也是自定义的，加入分组之前不需要提前创建，单Group ID的定义也要满足规则，如下所示。

> Group ID定义规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/meeting-demo-3.png" align="center" />

### 4. 互动体验

加入分组后，就可以体验基于分组的相关功能和特性了，包括音视频、屏幕共享、电子白板、文字聊天等等。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/meeting-demo-4.png" align="center" />


## RecordDemo

RecordDemo基于RESTFUL接口开发，用来演示云录制相关功能和特性。启动一个录制任务可以分为以下几个步骤：

### 1. 登录录制后台

对开发者ID和开发者秘钥进行鉴权。只有企业开发者才能够进行体验云录制功能，普通开发者和个人开发者暂不开放此能力。

> 私有云需要填写服务器地址，具体请咨询技术人员。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/record-demo-1.png" align="center" />

### 2. 查询录制任务

可以基于App ID、Group ID和Record State查询录制任务，其中App ID必填。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/record-demo-2.png" align="center" />

### 3. 创建录制任务

点击“创建”按钮，填入App ID和Group ID，用来指定录制哪个App下哪个分组。录制类型可以选择自动录制或手动录制，自动录制任务无需外部干预，基于内部预定义的布局进行录制与合成；手动录制任务需要开发者手动干预录制过程，选择需要录制哪一路媒体。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/record-demo-3.png" align="center" />

### 4. 控制录制任务

自动录制任务的控制比较简单，只能“暂停”或“停止”。手动录制任务的控制要稍微复杂些，需要手动指定需要录制的媒体，为了简化DEMO实现，当前不能自定义录制布局，使用预定义布局。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/record-demo-4.png" align="center" />

### 5. 管理录制文件

录制完成后，登录到管理后台，能够管理和下载录制文件。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/record-demo-5.png" align="center" />

## LiveDemo

LiveDemo基于RESTFUL接口开发，用来演示云直播相关功能和特性。启动一个直播分为以下几个步骤：

### 1. 登录控制后台

对开发者ID和开发者秘钥进行鉴权。只有企业开发者才能够进行体验云直播功能，普通开发者和个人开发者暂不开放此能力。

> 私有云需要填写服务器地址，具体请咨询技术人员。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/live-demo-1.png" align="center" />

### 2. 查询直播任务

支持基于App ID、Group ID和Live State来查询直播任务。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/live-demo-2.png" align="center" />

### 3. 创建直播任务

点击“创建”按钮，填入App ID和Group ID，便可创建指定分组的直播任务。创建直播前，需要保证分组已经存在，且分组内有人广播了媒体，比如音频、视频、屏幕共享等。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/live-demo-3.png" align="center" />

### 4. 观看直播

直播任务创建成功后，可以点击“观看”按钮立即播放直播视频，也可将直播链接拷贝到支持的播放器中进行播放。当前支持flv、rtmp和hls三种媒体格式，可以自由切换。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/demo/live-demo-4.png" align="center" />