# 快速开始

云录制相关业务功能需要客户的账号通过企业开发者的资格认证。认证成功就可以调用云录制api。
云录制接口是调用一套RESful Api来实现用户对录制业务的控制。

## 登录

云录制要通过登录接口来建立链接，。

### 请求参数说明

接口的请求类型为JSON。请求字段如下：

参数名 | 类型 | 是否必填 | 参数说明 
|- | - | - | - 
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4097 |
| app_id | String | 是 | 应用对应的appid |
| token | String | 是 | 应用通过token生成方式获得的值 |
| seq | String | 是 | 返回时会把此数据原样输出 |

示例：

```
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

```
//成功结果示例
{
"business":"RE",
"id":8193,
"msg":"10000",
"seq":"XXXXXXXXXXX",
}

//失败结果示例
{
"business":"RE",
"id":8193,
"msg":"10000",
"seq":"XXXXXXXXXXX",
}
```

## 初始化录制任务
建立长链接以后，可以开始为不同的分组初始化录制任务，设置录制任务的属性，比如格式、分辨率、帧率、录制模式等等。


### 请求参数说明

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4098 |
| group_id | String | 是 | 指定初始化录制任务的分组 |
| file_name | String | 否 | 不包含格式的录制文件名 |
| file_type | int | 否 | 0代表同时录制音视频的mp4格式，1代表仅录制音频的mp3格式，默认格式为mp4 |
| file_duration | int | 否 | 录制文件切片时长[15,300]（分钟min），默认为60分钟 |
| width | int | 否 | 幕布宽度[1px,1920px]默认1920px |
| height | int | 否 | 幕布高[1px,1080px]默认1080px |
| record_mode | int | 否 | 0代表合流（混流）模式 |
| frame_rate | int | 否 | 录制视频帧率(默认30帧)[1,30] |
| timeout | int | 否 | 该录制任务拉流失败超过timeout时间，且无录制命令，则服务器主动停止录制，[5,1800]默认值600 |
| seq | String | 是 | 返回时会把此数据原样输出 |


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
```
//成功结果示例
{
"business":"RE",
"id":8193,
"msg":"10000",
"seq":"XXXXXXXXXXX",
}

//失败结果示例
{
"business":"RE",
"id":8193,
"msg":"10000",
"seq":"XXXXXXXXXXX",
"record_id":"XXXXXXXXXXX"
}
```

## 恢复录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4099 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |




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


## 暂停录制任务

录制任务开始后，可随时暂停录制任务。暂停时的内容不会进行录制。

### 请求参数说明

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4100 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |



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



## 结束录制任务

结束录制任务以后会开始生成录制文件。

### 请求参数说明

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定填"RE" |
| id | int | 是 | 固定填4101 |
| record_id | String | 是 | 录制任务的ID  |
| seq | String | 是 | 返回时会把此数据原样输出 |



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


## 设置合成效果

设置视频的合成布局，音频的合成内容

### 请求参数说明

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
| media_type | int | 是 | 视频媒体类型  |
| x | int | 否 | 视频在幕布中横坐标[0,1920]，默认值0   |
| y | int | 否 | 视频在幕布中纵坐标[0,1080]，默认值0  |
| w | int | 否 | 视频的宽[1,1920]默认值320  |
| h | int | 否 | 视频的宽[1,1080]默认值240  |
| crop_mode | int | 否 | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为1  |


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


## 设置水印与字幕

支持在视频上叠加字幕

### 请求参数说明

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
| content | String | 否 | 字幕内容，默认为空 |
| color | int | 否 | 字幕颜色rgb，默认值0  |
| x | int | 否 | 字幕在幕布中横坐标[0,1920]，默认值0   |
| y | int | 否 | 字幕在幕布中纵坐标[0,1080]，默认值0  |
| transparency | int | 否 | 字幕透明度[0,100],0表示完全透明，100表示不透明;默认值100  |
| size | int | 否 | 字幕字体大小[1,200];默认值30  |


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


## 录制任务查询

可以查询当前已经初始化或正在进行的录制任务。

### 请求参数说明

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