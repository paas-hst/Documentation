# 快速开始

云直播相关业务功能需要客户的账号通过企业开发者的资格认证。认证成功就可以调用云直播api。
云直播接口是调用一套RESTful Api来实现用户对直播业务的控制。

简化步骤：

​       指定组开启直播                                         结束直播   

备注：组内先开始广播音视频或者屏幕共享流，再开启直播。

## 获取access_token

获取access_token，后续请求都是使用这个token;超时后需要重新获取。
使用方法为设置HTTP header.在HTTP请求头Authorization
 	Authorization:access_token

### 请求参数说明

请求地址：/access/token
HTTP协议，GET方法

参数名 | 类型 | 是否必填 | 参数说明 
| dev_id | String | 是 | 应用对应的开发者id |
| token | String | 是 | 应用通过token生成方式获得的值 |

说明：
Token生成方式参考我们官网提供的TokenGenerator

HTTP header.在HTTP请求头Authorization中携带开发者ID和Token，两者用”.”隔开，例如：
459d0e780b96ce2c42b6356a67e5e35c.k5FUR5LlEoTq5t1ZZ1A9RoQfqgbL1mtJ4DzMdwOW7tvaZZqhXtm6rsisnyoYo9S0HPTDBZGMMhii4gLAorBdCSxb0Iv0yBfFehUTW76gAUm7QuSo3ZqTMvsV
.前面 那一段是开发者ID，.后面的那一段是token..



示例：

```js
Authorization: 459d0e780b96ce2c42b6356a67e5e35c.k5FUR5LlEoTq5t1ZZ1A9RoQfqgbL1mtJ4DzMdwOW7tvaZZqhXtm6rsisnyoYo9S0HPTDBZGMMhii4gLAorBdCSxb0Iv0yBfFehUTW76gAUm7QuSo3ZqTMvsV
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| access_token | String | 令牌。后续的业务请求都用该令牌 |
| timeout | int | access_token超时时间，单位:秒 |


示例：

```js
//成功结果示例
{
	"code": 0,
	"msg": "OK",
	"result": {
		"timeout": 1000000,
		"access_token": "7bf93c4469ce312de23bf5d0e20a4f75"
	}
}

//失败结果示例

{
	"code": 606000001,
	"msg": "access_token timeout"
}

```



# 直播API



## 开始直播

请求地址：/v1/live/start  HTTP协议，POST方法


### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| group_id | String | 是 | 指定初始化录制任务的分组 |
| width | int | 否 | 幕布宽度[1,1920]（单位px）默认1920 |
| height | int | 否 | 幕布高[1,1080]（单位px）默认1080 |
| crop_mode | int | 否 | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为2  |
| frame_rate | int | 否 | 录制视频帧率(默认30帧)[1,30]（单位帧） |                                      |
| quality_level | int | 否 | 1 流畅、2 清晰、3高清 (默认2)|

请求示例：

```js
{
	"app_id":"XXXXXX",
	"group_id": "XXXX",
	"width": 1920,
	"height": 1080,
	"crop_mode":2,
	"quality_level":2,
	"frame_rate":20
}
```

### 返回说明

返回示例：

```js
{
	"code": 0,
	"flv_url": "http://xxxxxx.haoshitong.com/fsp-live/20200512161527_1111.flv",
	"group_id": "1111",
	"m3u8_url": "http://xxxx.haoshitong.com/fsp-live/20200512161527_1111.m3u8",
	"msg": "success",
	"rtmp_url": "rtmp://xxxx.haoshitong.com/fsp-live/20200512161527_1111"
}
```
## 关闭直播

请求地址：/v1/live/stop  HTTP协议，POST方法


### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |
| group_id | String | 是 | 指定初始化录制任务的分组 |

请求示例：

```js
{
	"app_id":"XXXXXX",
	"group_id": "XXXX"
}
```

### 返回说明

返回示例：

```js
{
	"code": 0,
	"group_id": "1111",
	"msg": "stop live success"
}
```

## 获取直播列表

请求地址：/v1/live/list  HTTP协议，Get方法

### 请求参数说明

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| app_id | String | 是 | 应用ID |

请求示例：

```js
/v1/live/list?app_id=xxxxx
```

### 返回说明

返回示例：

```js
{
	"code": 0,
	"id": 9475,
	"list": [{
		"flv_url": "http://live.alicdn.haoshitong.com/fsp-live/20200513112347_1111.flv",
		"group_id": "1111",
		"m3u8_url": "http://live.alicdn.haoshitong.com/fsp-live/20200513112347_1111.m3u8",
		"rtmp_url": "rtmp://live.alicdn.haoshitong.com/fsp-live/20200513112347_1111",
		"start_time": 1589340227
	}],
	"msg": "success"
}
```

错误码 | 描述  
|- | - | 
| 6050030000| 异常失败 | 
| 6050030001| 上下文不存在 | 
| 6050030003|参数错误 |
| 6050030004|链接已经存在|
| 6050030005|json解析错误| 
| 6050030006|未登录   |
| 6050030007|鉴权失败|
| 6050030008|剩余空间不足  |
| 6050030009 6050030010 6050030011|服务器上下文已达负载上限  |
| 6050030012|上下文已经存在 |
| 6050030013|虚拟用户登录失败| 
| 6050030016|给资源平台发送命令失败|
| 6050030017|解析资源平台消息错误 |
| 6050030018|资源平台record 响应返回失败  |
| 6050030020|创建输入通道失败，没有Parameter参数|
| 6050030021|创建输入通道失败，输入通道已经存在  
| 6050030022|移除输入通道失败，不存在指定的输入通道|
| 6050030023|设置输出参数失败，媒体服务器内部原因|
| 6050030024|设置输出参数失败，不存在指定的输入通道或者输入同道类型不对|
| 6050030025|设置输出参数失败，设置了幕布大小却没有设置布局|
| 6050030026|设置输出参数失败，没有设置幕布大小却设置布局|
| 6050030027|设置输出叠加台标字幕失败，媒体服务器内部原因|
| 6050030028|认证失败 |
| 6050030029|心跳异常|
| 6050030031|文件读取异常|
| 6050030032|媒体服务返回超时    |
| 6050030033|直播任务暂停，设置输出失败|
| 6050030034|下载中间文件失败|
| 6050030035|自动直播不支持 手动设置布局|
| 6050030036|自动直播 登陆事件网关失败   |
| 6050030038|自动直播 该房间存在一个自动直播任务    |
| 6050030039|不能暂停  直播中才可以   |
| 其他错误码 | 重新请求依然有问题时，请联系服务提供商 |
