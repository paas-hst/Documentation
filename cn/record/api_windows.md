# 快速开始

云录制相关业务功能需要客户的账号通过企业开发者的资格认证。认证成功就可以调用云录制api。
云录制接口是调用一套RESTful Api来实现用户对录制业务的控制。

## 登录

通过登录接口完成长链接的建立。后续的接口都依赖登录完成。


### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4097 |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：

```js
{
"business":"RE",
"app_id":"323f848115e3d0249289fa37685a7c31",
"token":"XXXXXXXX",
"seq":"1",
"id":4097
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 返回固定为8193 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |

示例：

```js
//成功结果示例
{
"business":"RE",
"id":8193,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
}

//失败结果示例
{
"business":"RE",
"id":8193,
"code":30008,
"msg":"10000",
"seq":"XXXXXXXXXXX",
}
```

## 初始化录制任务


建立长链接以后，可以开始为不同的分组初始化录制任务，设置录制任务的属性，比如格式、分辨率、帧率、录制模式等等。


### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4098 |
| group_id | String | 是 | 指定初始化录制任务的分组 |
| file_name | String | 否 | 不包含格式的录制文件名 |
| file_type | int | 否 | 0代表同时录制音视频的mp4格式，1代表仅录制音频的mp3格式，默认格式为mp4 |
| file_duration | int | 否 | 录制文件切片时长[15,300]（分钟min），默认为60分钟 |
| width | int | 否 | 幕布宽度[1,1920]（单位px）默认1920 |
| height | int | 否 | 幕布高[1,1080]（单位px）默认1080 |
| record_mode | int | 否 | 0代表合流（混流）模式 |
| frame_rate | int | 否 | 录制视频帧率(默认30帧)[1,30]（单位帧） |
| timeout | int | 否 | 该录制任务拉流失败超过timeout时间，且无录制命令，则服务器主动停止录制，[5,1800]（单位秒）默认值600秒 |
| auto | Array | 否 | 不为空时使用自动录制 |
| seq | String | 是 | 返回时会把此数据原样输出 |

auto视频列表的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| type | int | 否 | 1:均分,2:主从;默认1 |
| user_id | String | 否 | type=2时需要设置，没有的话则会默认使用第一个进入分组的用户ID |
| media_type | int | 否 | 媒体顺序。2:优先级按屏幕共享>摄像头>白板的顺序。  |
| media_count | int | 否 | 范围[1,9]，代表自动录视频数最多不超过的路数  |
| crop_mode | int | 否 | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为1  |

示例：
```js
//手动录制
{
"business":"RE",
"id":4098,
"group_id":"XXXXXXXX",
"file_name":"XXXXXXXX",
"file_type":0,
"file_duration":15,
"width":10,
"height":10,
"record_mode":0,
"frame_rate":30,
"timeout":10,
"seq":"1",
}

//自动录制
{
"business":"RE",
"id":4098,
"group_id":"XXXXXXXX",
"file_name":"XXXXXXXX",
"file_type":0,
"file_duration":15,
"width":10,
"height":10,
"record_mode":0,
"frame_rate":30,
"timeout":10,
"auto":{"type":1,"user_id":2,"media_type":2,"media_count":9,"crop_mode":3},
"seq":"1",
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8193 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8193,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8193,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 恢复录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4099 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：
```js
{
"business":"RE",
"id":4099,
"record_id":"XXXXXXXX",
"seq":"1",
}
```


### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8195 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8195,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8195,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 暂停录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4100 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：
```js
{
"business":"RE",
"id":4100,
"record_id":"XXXXXXXX",
"seq":"1",
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8196 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8196,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8196,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 结束录制任务

结束录制任务以后会开始生成录制文件。

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4101 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：
```js
{
"business":"RE",
"id":4101,
"record_id":"XXXXXXXX",
"seq":"1",
}
```


### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8197 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| media_duration | int | 视频时长 |
| record_duration | int | 录制任务时长 |
| flow | int | 录制花费总流量（kb） |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8197,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8197,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 设置合成效果

设置视频的合成布局样式，以及指定音频合成路数。非自动录制时，首次设置合成效果代表开始录制。
没有任何可录制音视频时，不会进行合成。

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4102 |
| record_id | String | 是 | 录制任务的ID  |
| audio_list | Array | 否 | 音频列表  |
| video_list | Array | 否 | 视频列表  |
| seq | String | 是 | 返回时会把此数据原样输出 |

audio_list音频列表的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| user_id | String | 是 | 音频流所属用户的ID |
| media_id | String | 是 | 音频id |
| media_type | int | 否 | 目前音频类型只有一种：1  |

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
"business":"RE
"id":"4102",
"record_id":"XXXXXXXX",
"audio_list":{
	{"user_id":"Jack_ID","media_id":1},
	{"user_id":"Paul_ID","media_id":1}
	},
"video_list":{
	{"user_id":"Jack_ID","media_id":0,"media_type":2,"crop_mode":3,"w":530,"h":380},
	{"user_id":"Paul_ID","media_id":0,"media_type":2,"crop_mode":3,"x":531,"w":530,"h":380}
	},
"seq":""
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8198 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8198,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8198,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```


## 设置水印与字幕

支持在视频上叠加字幕

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4103 |
| record_id | String | 是 | 录制任务的ID  |
| subtitle_list | Array | 否 | 视频字幕列表  |
| seq | String | 是 | 返回时会把此数据原样输出 |

subtitle_list字幕的请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| type | int | 否 | 1:静态文本,2:动态系统时间；默认为1 |
| content | String | 否 | 字幕内容，默认为空。type为2时不用填能内容 |
| color | int | 否 | 字幕颜色rgb，默认值0  |
| x | int | 否 | 字幕在幕布中横坐标[0,1920]，默认值0   |
| y | int | 否 | 字幕在幕布中纵坐标[0,1080]，默认值0  |
| transparency | int | 否 | 字幕透明度[0,100],0表示完全透明，100表示不透明;默认值100  |
| size | int | 否 | 字幕字体大小[1,200];默认值30  |

示例：
```js
{
"business":"RE",
"id":"4103",
"record_id":"XXXXXXXX",
"subtitle_list":{
	{"type":1,"content":"Jack","color":#009cff,"x":20,"y":50,"transparency":80,"size":25}
	},
"seq":""
}
```

### 返回说明
接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8199 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| seq | String | 用户请求时填写的数据 |
| record_id | String | 返回录制任务唯一身份识别ID |

示例：
```js
//成功结果示例
{
"business":"RE",
"id":8199,
"code":0,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}

//失败结果示例
{
"business":"RE",
"id":8199,
"code":30001,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 录制任务查询

可以查询当前已经初始化或正在进行的录制任务。

### 请求参数说明

请求地址：ws://fsp-record-gw.hst.com/
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4104 |
| record_id | String | 否 | 需要查询的录制任务ID  |
| group_id | String | 否 | 需要查询的组ID  |
| status | int | 否 | 按任务状态过滤。1:初始化,2:录制中,3:排队等待编码,4:编码中,5:上传中,6:完成,-1:任务异常  |
| start_time | date | 否 | 任务开启时间  |
| stop_time | date | 否 | 任务结束时间  |
| page | int | 否 | 查询第几页；默认第一页 |
| page_size | int | 否 | 每页显示条数[1,500]默认值50 |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：

```js
{
"business":"RE",
"seq":"1",
"id":4104
}
```

### 返回说明
接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| business | String | 固定为"RE" |
| id | int | 登录的返回固定为8200 |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示的消息 |
| record_list | Array | 返回的消息 |
| total_num | int | 总条数 |
| seq | String | 用户请求时填写的数据 |

record_list录制任务列表的返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - |
| record_id | String | 录制任务ID |
| record_mode | int | 录制模式 |
| group_id | int | 组ID |
| start_time| date | 任务开启时间 |
| stop_time | date | 任务结束时间 |
| status | int | 任务状态  |


# 存储接口

发post请求，form-data格式的数据。

## 查询录制文件

请求地址：https://fsp-store-gw.hst.com/api/record/file/list

### 请求参数说明

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 不做校验，填"RE" |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |
| file_name | String | 否 | 完全匹配 |
| file_state | String | 否 | 录制状态 |
| page | int | 否 | 页码 |
| page_size | int | 否 | 每页多少条数据 |
| start_time | date格式的string | 否 | 开始时间，建议填写。不填写只查询默认30天的范围 |
| end_time | date格式的string| 否 | 结束时间，建议填写。不填写只查询默认30天的范围 |


### 返回说明

返回示例：

```js
{
    "code": 0,
    "message": "OK",
    "data": {
        "count": 2,
        "dataList": [
            {
                "resourceName": "20190712110046_10050",
                "fileLength": XXXXXX,
                "fileState": "normal",
                "fileSize": XXXXXX,
                "resourceType": ".mp4",
                "recordTime": "2019-07-01 11:00:46"
            },
            {
                "resourceName": "XXXXXXXXXXXXX",
                "fileLength": XXXXXX,
                "fileState": "normal",
                "fileSize": XXXXXX,
                "resourceType": ".mp3",
                "recordTime": "2019-07-02 17:58:02"
            }
        ]
    }
}
```
count代表总共有多少条
resourceName代表文件的名称
fileLength代表文件总时长，单位是秒。
fileState代表当前的状态。creating 初始化；uploading 上传中；normal  完成，可下载；exception 异常。
fileSize是文件大小，单位是Byte。
resourceType是文件类型，目前有mp3、mp4两种。
recordTime是录制任务开始时间。

## 查询存储空间

请求地址：https://fsp-store-gw.hst.com/api/store/volume/getUsedVolume

### 请求参数说明

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 不做校验，填"RE" |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |


### 返回说明

返回示例：

```js
{
    "code": 0,
    "message": "OK",
    "data": {
        "volume": 21474836480,
        "useVolume": 7815569
    }
}
```
volume代表总空间，单位Byte（如果没有设置最大使用空间返回为-1）
usevolume代表已使用空间，单位Byte（如果没有开通最大使用空间返回为-1）


## 获取存储文件下载链接

请求地址：https://fsp-store-gw.hst.com/api/record/file/download
下载某个具体文件的内容，如果文件有多个分片则会返回多条记录。

### 请求参数说明

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 不做校验，填"RE" |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |
| file_name | String | 是 | 完全匹配，如果不存在则返回为空 |

### 返回说明

返回示例：

```js
{
    "code": 0,
    "message": "OK",
    "data": {
        "urls": "http://XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
		"count": 1
    }
}
```

urls代表下载链接。需要在1个小时内请求下载。下载时间超过1个小时没影响，但没办法再次请求。
count代表可下载分片文件总数，可通过http请求下载。


## 删除文件

请求地址：https://fsp-store-gw.hst.com/api/record/file/delete
文件删除成功和文件不存在都是返回ok，data为空。

### 请求参数说明

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 不做校验，填"RE" |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |
| file_name | String | 是 | 完全匹配 |

### 返回说明

返回示例：

```js
{
    "code": 0,
    "message": "OK",
    "data": null
}
```

## 错误码


错误码 | 描述  
|- | - | 
| 30000 | 异常失败 | 
| 30001 | 上下文不存在 | 
| 30003 | 命令参数错误 | 
| 30004 | app_id已登录(目前同时只能建立一个链接) | 
| 30005 | Json解析失败 | 
| 30006 | 未登录 | 
| 30007 | 鉴权失败 |
| 30011 | 已到达客户设置的硬盘上限 | 
| 30035 | 自动录制不支持设置布局 |
| 30038 | 一个房间只允许有一个自动录制任务 |
| 其他错误码 | 重新请求依然有问题时，请联系服务提供商 |

