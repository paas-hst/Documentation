# 快速开始

云直播相关业务功能需要客户的账号通过企业开发者的资格认证。认证成功就可以调用云直播api。
云直播接口是调用一套RESTful Api来实现用户对直播业务的控制。

简化步骤：

 直        播：开启直播                                         结束直播   

备注：组内先开始广播音视频或者屏幕共享流，再开启直播。

## 获取access_token

获取access_token，后续请求都是使用这个token;超时后需要重新获取。
使用方法为设置HTTP header.在HTTP请求头Authorization
 	Authorization:$access_token

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

| 参数名       | 类型   | 参数说明                       |
| ------------ | ------ | ------------------------------ |
| access_token | String | 令牌。后续的业务请求都用该令牌 |
| timeout      | int    | access_token超时时间，单位:秒  |


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

| 参数名        | 类型   | 是否必填 | 参数说明                                                  |
| ------------- | ------ | -------- | --------------------------------------------------------- |
| app_id        | String | 是       | 应用ID                                                    |
| group_id      | String | 是       | 指定初始化直播任务的分组                                  |
| width         | int    | 否       | 幕布宽度[1,1920]（单位px）默认320                         |
| height        | int    | 否       | 幕布高[1,1080]（单位px）默认240                           |
| crop_mode     | int    | 否       | 视频裁剪模式(1:平铺;2:等比平铺裁剪;3:等比平铺填充)默认为2 |
| frame_rate    | int    | 否       | 直播视频帧率(默认30帧)[1,30]（单位帧）                    |
| quality_level | int    | 否       | 1 流畅、2 清晰、3高清 (默认2)                             |

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

| 参数名   | 类型   | 参数说明           |
| -------- | ------ | ------------------ |
| code     | int    | 操作结果 0为成功   |
| group_id | String | 直播的组id         |
| flv_url  | String | flv格式的拉流地址  |
| m3u8_url | String | m3u8格式的拉流地址 |
| rtmp_url | String | rtmp格式的拉流地址 |
| msg      | String | 成功为success      |

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

| 参数名   | 类型   | 是否必填 | 参数说明                 |
| -------- | ------ | -------- | ------------------------ |
| app_id   | String | 是       | 应用ID                   |
| group_id | String | 是       | 指定初始化直播任务的分组 |

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

| 参数名 | 类型   | 是否必填 | 参数说明 |
| ------ | ------ | -------- | -------- |
| app_id | String | 是       | 应用ID   |

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

