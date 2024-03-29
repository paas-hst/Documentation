# 录制API



## 初始化录制任务


可以开始为不同的分组初始化录制任务，设置录制任务的属性，比如格式、分辨率、帧率、录制模式等等。


### 请求参数说明

请求地址：/v1/record/init
HTTP body, Content-Type为application/json;charset=UTF-8

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| group_id | String | 是 | 指定初始化录制任务的分组 |
| file_name | String | 否 | 不包含格式的录制文件名 |
| file_type | int | 否 | 0代表同时录制音视频的mp4格式，1代表仅录制音频的mp3格式，默认格式为mp4 |
| file_duration | int | 否 | 录制文件切片时长[15,300]（分钟min），默认为60分钟 |
| width | int | 否 | 幕布宽度[1,1920]（单位px）默认1920 |
| height | int | 否 | 幕布高[1,1080]（单位px）默认1080 |
| record_mode | int | 否 | 0代表合流（混流）模式 |
| frame_rate | int | 否 | 录制视频帧率(默认30帧)[1,30]（单位帧） |
| timeout | int | 否 | 该录制任务拉流失败超过timeout时间，且无录制命令，则服务器主动停止录制，[5,1800]（单位秒）默认值600秒 |
| auto | Object | 否 | 不为空时使用自动录制 |
| seq | String | 是 | 返回时会把此数据原样输出 |
| company_id | String | 是 | 公司ID |
auto的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| type | int | 否 | 1:均分,2:主从;默认1 |
| user_id | String | 否 | type=2时需要设置，没有的话则会默认使用第一个进入分组的用户ID |
| media_type | int | 否 | 媒体顺序。2:优先级按屏幕共享>摄像头>白板的顺序。  |
| media_count | int | 否 | 范围[1,9]，代表自动录视频数最多不超过的路数  |
| crop_mode | int | 否 | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为2  |

示例：
```js
//手动录制
{
"app_id":"XXXXXXXX",
"group_id":"XXXXXXXX",
"file_name":"XXXXXXXX",
"file_type":0,
"file_duration":15,
"width":1280,
"height":720,
"record_mode":0,
"frame_rate":30,
"timeout":10
}

//自动录制
{
"app_id":"XXXXXXXX",
"group_id":"XXXXXXXX",
"file_name":"XXXXXXXX",
"company_id":1234,
"auto":{}
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| id | int | 登录的返回固定为8194 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```

## 恢复录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

请求地址：/v1/record/resume
HTTP body, Content-Type为application/json;charset=UTF-8
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| record_id | String | 是 | 录制任务的ID  |
| app_id | String | 是 | 应用ID |

示例：
```js
{
"record_id":"XXXXXXXX",
"app_id":"XXXXXXXX",
}
```


### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```

## 暂停录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

请求地址：/v1/record/suspend  HTTP协议，POST方法
HTTP body, Content-Type为application/json;charset=UTF-8
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| record_id | String | 是 | 录制任务的ID  |
| app_id | String | 是 | 应用ID |

示例：
```js
{
"record_id":"XXXXXXXX",
"app_id":"XXXXXXXX",
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```

## 结束录制任务

结束录制任务以后会开始生成录制文件。

### 请求参数说明

请求地址：/v1/record/finish HTTP协议，POST方法
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| record_id | String | 是 | 录制任务的ID  |
| app_id | String | 是 | 应用ID |

示例：
```js
{
"app_id":"XXXXXXXX",
"record_id":"XXXXXXXX",
}
```


### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| media_duration | int | 视频时长 |
| record_duration | int | 录制任务时长 |
| flow | int | 录制花费总流量（kb） |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX",
"media_duration":79
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```

## 设置合成效果

设置视频的合成布局样式，以及指定音频合成路数。非自动录制时，首次设置合成效果代表开始录制。
没有任何可录制音视频时，不会进行合成。

### 请求参数说明

请求地址：/v1/record/set/layout  HTTP协议，POST方法
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| record_id | String | 是 | 录制任务的ID  |
| audio_list | Array | 否 | 音频列表  |
| video_list | Array | 否 | 视频列表  |
| seq | String | 是 | 返回时会把此数据原样输出 |

audio_list音频列表的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| user_id | String | 是 | 音频流所属用户的ID |
| media_id | String | 是 | 音频id |
| media_type | int | 是 | 目前音频类型只有一种：1  |

video_list视频列表的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| user_id | int | 是 | 视频流所属用户的ID |
| media_id | String | 是 | 视频id |
| media_type | int | 是 | 视频媒体类型,0固定为屏幕共享,2位摄像头  |
| x | int | 否 | 视频在幕布中横坐标[0,1920]，默认值0   |
| y | int | 否 | 视频在幕布中纵坐标[0,1080]，默认值0  |
| w | int | 否 | 视频的宽[1,1920]默认值320  |
| h | int | 否 | 视频的宽[1,1080]默认值240  |
| crop_mode | int | 否 | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为1  |

示例：
```js
{
"app_id":"XXXXXXXX",
"record_id":"XXXXXXXX",
"audio_list":{
	{"user_id":"Jack_ID","media_id":"appdef_mic","media_type":1},
	{"user_id":"Paul_ID","media_id":"appdef_mic","media_type":1}
	},
"video_list":{
	{"user_id":"Jack_ID","media_id":"LocalCam_0","media_type":2,"crop_mode":3,"w":530,"h":380},
	{"user_id":"Paul_ID","media_id":"LocalCam_0","media_type":2,"crop_mode":3,"x":531,"w":530,"h":380}
	}
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```
## 设置文字水印
在视频上面指定位置设置一下文字说明


### 请求参数说明

请求地址：/v1/record/set-output-overlay  HTTP协议，POST方法
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| record_id | String | 是 | 录制任务的ID  |
| subtitle_list | Array | 否 | 文字水印列表  |
| logo_list | Array | 否 |  图片水印列表（未开放外部使用）  |

subtitle_list文字水印列表的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| x | int | 是 | 幕布中横坐标[0,1920]  |
| y | int | 是 | 幕布中横坐标[0,1920]  |
| content | String | 是 | 需要显示的文字  |
| color | int | 是 | 文字颜色  |
| size | int | 是 | 文字大小  |
| transparency | int | 是 | 透明度 |

logo_list水印列表的请求字段如下：
| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| x | int | 是 | 幕布中横坐标[0,1920]  |
| y | int | 是 | 幕布中横坐标[0,1920]  |
| file_path | String | 是 | 服务器上图片的路径  |
| scaleratio | float | 是 | 缩放比例  |


示例：
```js
{
        "id": 4103,
        "logo_list": [{
                "x": 1240,
                "y": 1240,
                "file_path": "bg/720P/4_640x360_able.png",
                "scaleratio": 1
        }],
        "subtitle_list": [{
                "type": 1,
                "x": 1240,
                "y": 1240,
                "content": "",
                "color": 255,
                "size": 30,
                "transparency": 50
        }]
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"code":0,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"code":30001,
"msg":"10000",
"record_id":"XXXXXXXXXXX"
}
```


## 录制任务查询

可以查询当前已经初始化或正在进行的录制任务。

### 请求参数说明

请求地址：/v1/record/task/list  HTTP协议，GET方法
请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| record_id | String | 否 | 需要查询的录制任务ID  |
| group_id | String | 否 | 需要查询的组ID  |
| status | int | 否 | 按任务状态过滤。1:初始化,2:录制中,3:排队等待编码,4:编码中,5:上传中,6:完成,-1:任务异常  |
| start_time | date | 否 | 任务开启时间  |
| stop_time | date | 否 | 任务结束时间  |
| page | int | 否 | 查询第几页；默认第一页 |
| page_size | int | 否 | 每页显示条数[1,500]默认值50 |

示例：

```js

http://localhost:8080/v1/record/task/list?app_id=123&group_id=record

```

### 返回说明
接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| record_list | Array | 返回的消息 |
| total_num | int | 总条数 |

record_list录制任务列表的返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - |
| record_id | String | 录制任务ID |
| record_mode | int | 录制模式 |
| group_id | int | 组ID |
| start_time| date | 任务开启时间 |
| stop_time | date | 任务结束时间 |
| status | int | 任务状态  |
| file_name | String | 文件名  |
| company_id | String |  公司ID  |
| record_time | int |  录制时长(秒)  |
| width | int |  视频宽  |
| height | int |  视频高  |


## 获取下载录制文件的URL

请求地址：/v1/record/file/download/url HTTP协议，GET方法

### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用对应的appid |
| record_id | String | 是 | 录制ID |
| page | int | 否 | 页码 |
示例：

```js

http://localhost:8080/v1/record/file/download/url?app_id=123&record_id=record

```

### 返回说明
| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| total_num | int | 是 | 多少个文件即data_list的数量 |
| data_list | Array | 是 | 录制文件链接数组 |
| page | int | 否 | 页码 |

data_list  录制文件下载链接列表的返回字段如下：
| 参数名 | 类型 | 参数说明 |
| - | - | - |
| url | String | 下载地址 |
| md5 | int | 录制文件的md5值 |
| file_name | int | 最开始初始化设置的文件名 |
| extent| date | 扩展字段 |
| play_url| string | 点播地址(私有云部署且文件是MP4才有) |

返回示例：

```js
{
    "total_num": 0,
	"page":0,
    "msg": "OK",
    "data_list": [
		{
			"url": "xxxxxxx",
			"md5": "XXXXXX",
			"file_name": "xxx",
			"extent": "XXXXXX"
		},
		{
			"url": "xxxxxxx",
			"md5": "XXXXXX",
			"file_name": "xxx",
			"extent": "XXXXXX"
		}
    ]
}
```

## 删除文件

请求地址：/v1/record/file  HTTP协议，POST方法
文件删除成功和文件不存在都是返回ok，data为空。

### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| mode | String | 是 | 删除模式（1：同时删除源文件和录制记录；2：只删除源文件; 3: 只删除录制任务记录）|
| app_id | String | 是 | 应用对应的appid |
| record_list | Array | 是 | 录制任务ID列表 |

请求示例：

```js
{
	"mode" :1,
	"app_id":"97017e465d19b62033ab4e13680e3028",
	"record_list":["20200220115205_10001"]
}
```

### 返回说明

返回示例：

```js
{
	"code":0,
	"msg":"ok"
}
```
## 获取录制详情（未开放）

请求地址：/v1/record/info  HTTP协议，POST方法
文件删除成功和文件不存在都是返回ok，data为空。

### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用对应的appid |
| record_id | String | 是 | 录制任务ID列表 |

请求示例：

```js
{
	"app_id":"97017e465d19b62033ab4e13680e3028",
	"record_id":"20200220115205_10001"
}
```

### 返回说明
| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String  | 固定是RE |
| code | Int  | 成功为0 其他为失败的错误码 |
| create_time | String  | 录制创建时间 |
| file_name | String  | 录制文件名 |
| height | String  | 视频高 |
| width | String  | 视频宽 |
| msg | String  | 成功为SUCESS  错误时的错误描述 |
| record_id | String  | 录制ID |
| status | int  | 录制状态 |
| room_id | string  | 房间ID |
| record_file | Array  | 录制文件信息列表 |


record_file  录制文件下载链接列表的返回字段如下：
| 参数名 | 类型 | 参数说明 |
| - | - | - |
| duration | String | 视频时长 |
| file_id | int | 合成文件ID |
| size | int | 文件大小(byte) |
| start_time| date | 视频开始时间 |
| thumbnail_id| string | 视频缩略图文件ID |
返回示例：

```js
{
	"business": "RE",
	"code": 0,
	"create_time": "2021-08-14 10:51:10",
	"file_name": "-",
	"height": 1080,
	"id": 8213,
	"msg": "SUCESS",
	"record_file": {
		"duration": 31,
		"file_id": "cdeffc32057268dc8b182014dfc25d80",
		"size": 5531857,
		"start_time": "2021-08-14 10:51:10",
		"thumbnail_id" : "b06a38b96f546ff7bf4cf91329ca9277"
	},
	"record_id": "20210814105110_10000_control1",
	"status":6,
	"room_id": "",
	"width": 1920
}

```