# 业务网关接口

## 创建应用

### 请求方式
HTTP或HTTPS协议，POST方法

### 资源路径
/v1/app

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| app_name | String | 是 | 应用名称。只允许中英文、下划线 |
| status | String | 否 | 应用状态。online:上线；offline下线。默认下线 |
| consumption_limit | int | 否 | 消费限额。单位：元 |
| service | List/Array | 是 | 应用的服务配置 |
service中的对象：
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| service_id | int | 是 | 服务ID。3：视频服务；4：音频服务；5：屏幕共享服务；6：信令通道服务；7：在线服务；8：录制服务；9：微信小程序服务 |
| use_limit | long | 否 | 使用限量 |

### 传参方式
HTTP body, Content-Type为application/json;charset=UTF-8

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| app_id | String | 应用唯一标识 |
| app_secret | String | 应用秘钥 |
| app_name | String | 应用名称 |
| status | String | 应用状态。online:上线；offline:下线 |
| consumption_limit | int | 消费限额。单位：元 |
| service | List/Array | 是 | 应用的服务配置 |
service中的对象：
| 参数名 | 类型 | 参数说明 |
| :-: | :-: | - |
| service_id | int | 服务ID。3：视频服务；4：音频服务；5：屏幕共享服务；6：信令通道服务；7：在线服务；8：录制服务；9：微信小程序服务 |
| service_name | String | 服务名称 |
| use_limit | long | 使用限量 |

## 修改应用配置

### 请求方式
HTTP或HTTPS协议，PATCH方法

### 资源路径
/v1/app

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| app_id | String | 是 | 应用标识 |
| app_name | String | 否 | 应用名称。只允许中英文、下划线 |
| status | String | 否 | 应用状态。online:上线；offline下线。默认下线 |
| consumption_limit | int | 否 | 消费限额。单位：元 |
| service | List/Array | 否 | 应用的服务配置 |
service中的对象：
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| service_id | int | 是 | 服务ID。3：视频服务；4：音频服务；5：屏幕共享服务；6：信令通道服务；7：在线服务；8：录制服务；9：微信小程序服务 |
| use_limit | long | 否 | 使用限量 |

### 传参方式
HTTP body, Content-Type为application/json;charset=UTF-8

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| app_id | String | 应用唯一标识 |
| app_secret | String | 应用秘钥 |
| app_name | String | 应用名称 |
| status | String | 应用状态。online:上线；offline:下线 |
| consumption_limit | int | 消费限额。单位：元 |
| service | List/Array | 应用的服务配置 |
service中的对象：
| 参数名 | 类型 | 参数说明 |
| :-: | :-: | - |
| service_id | int | 服务ID。3：视频服务；4：音频服务；5：屏幕共享服务；6：信令通道服务；7：在线服务；8：录制服务；9：微信小程序服务 |
| service_name | String | 服务名称 |
| use_limit | long | 使用限量 |

## 删除应用

### 请求方式
HTTP或HTTPS协议，DELETE方法

### 资源路径
/v1/app

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| app_id | String | 是 | 应用标识 |

### 传参方式
URL传参，例如：http://your-server-ip:28000/v1/app?app_id=123

### 响应结果
只有上述通用部分的响应结果

## 获取计费话单列表

### 请求方式
HTTP或HTTPS协议，GET方法

### 资源路径
/v1/consuming/records

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| start_time | long | 是 | 开始时间，单位：毫秒 |
| end_time | long | 是 | 结束时间，单位：毫秒 |
| app_id | String | 否 | 应用ID |
| page | int | 是 | 页码 |
| page_size | int | 是 | 每页显示的数目，不能超过100 |

### 传参方式
URL传参，例如：http://your-server-ip:28000/v1/consuming/records?start_time=1588146896000&end_time=1590738896000&page=1&page_size=10

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| app_id | String | 应用唯一标识 |
| app_name | String | 应用名称 |
| product_id | int | 产品ID |
| product_name | String | 产品名称 |
| amount | double | 金额，单位：元 |
| price | double | 价格，单位：元 |
| charge_term | int | 计费项。1、音频通信话单；2、视频通信话单；4、屏幕共享话单；6信令次数话单；7、最大在线人数话单；8、录制分辨率路数时长话单；9、录制存储容量话单；10、录制流量话单；11、微信小程序语音话单；12、微信小程序视频话单 |
| start_time | String | 开始时间 |
| end_time | String | 结束时间 |
| total_time | int | 总时长，单位：秒 |
| group_id | String | 组ID |
| resolution | String | 分辨率 |
| total_sig_num | long | 信令个数 |
| stream_id | String | 流ID |
| client_id | String | 客户端ID |
| transfer_type | int | 传输类型，1：上行；2：下行 |

## 踢出用户

### 请求方式
HTTP或HTTPS协议，POST方法

### 资源路径
/v1/kickout

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| app_id | String | 是 | 应用唯一标识 |
| user_id | String | 是 | 用户ID |
| mutex_type | String | 否 | 终端互斥类型 |

### 传参方式
HTTP body, Content-Type为application/json;charset=UTF-8

### 响应结果
只有上述通用部分的响应结果

## 从在线获取用户状态

### 请求方式
HTTP或HTTPS协议，GET方法

### 资源路径
/v1/online/user/state

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| company_id | String | 否 | 企业ID |
| page | int | 否 | 页码 |
| page_size | int | 否 | 每页显示的数目 |
| app_id | String | 是 | 应用唯一标识 |
| msg_id | int | 是 | 消息唯一标识。由调用方自定义，服务端会原封不动返回 |

### 传参方式
URL传参，例如：http://your-server-ip:28000/v1/online/user/state?company_id=123&page=1&page_size=10

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| msg_id | int | 消息唯一标识 |
| user_list | List/Array | 用户列表 |
user_list中的对象：
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| state | int | 用户状态。0不在线；1在线 |
| user_id | String | 用户ID |
| terminal_seq_num | String | 终端标识 |
| mutex_type | String | 终端互斥类型 |

## 下发指令给终端

### 请求方式
HTTP或HTTPS协议，POST方法

### 资源路径
/v1/online/trans-cmd

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| user_list | List/Array | 是 | 用户列表 |
| trans_mess | Object | 是 | 给终端传递的信息，由调用方定义 |
| app_id | String | 是 | 应用ID |
| msg_id | int  | 是 | 消息唯一标识。消息唯一标识 |
user_list中的对象：
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| user_id | String | 是 | 用户ID |
| mutex_type | String | 是 | 终端互斥类型 |
| client_guid | String | 是 | 客户端标识 |

### 传参方式
HTTP body, Content-Type为application/json;charset=UTF-8

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| msg_id | int | 消息唯一标识 |
| user_list | List/Array | 用户列表 |
user_list中的对象：
| 参数名 | 类型 | 参数说明 |
| :-: | :-: | - |
| result | int | 0:成功;1:异常;2:该用户对应的设备不在线 |
| user_id | String | 用户ID |
| terminal_seq_num | String | 终端标识 |
| mutex_type | String | 终端互斥类型 |

## WEB在线邀请

### 请求方式
HTTP或HTTPS协议，POST方法

### 资源路径
/v1/online/invite

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| app_id | String | 是 | 应用唯一标识 |
| group_id | String | 是 | 组ID/会议ID |
| user_id_list | List/Array | 是 | 所呼叫的用户的ID列表。例如[“123”,”abc”] |
| seq_id | long | 是 | 请求的唯一标识 |
| extend_info | Object | 否 | 扩展内容 |

### 传参方式
HTTP body, Content-Type为application/json;charset=UTF-8

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| seq_id | long | 请求的唯一标识 |
| user_id_list | List/Array | 发送失败的用户的ID列表 |






 <center> <font face="黑体" size=10>  事件网关接口  </font>  </center>





>简化步骤：
>​         登录网关（保持长连接）：获取全量，订阅app事件，接收事件推送消息， 取消订阅app事件，退出登录。



##  获取服务器请求地址
> 公有云：使用接口 https://access.paas.haoshitong.com/server/address?appType=8 获取
> 私有云: 使用接口 https://私有云fsp地址:21000/server/address?appType=8        获取

接口的返回类型为JSON。返回字段如下：
| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| code | int | 登录的返回固定为20001 |
| result | string | 服务地址 |
| message | String | 提示的消息 |
示例：
```js
{
	"code": 0,
	"message": "OK",
	"result": "ws://192.168.7.201:29200"
}
```


## 登录事件网关
> 登录之后保持长连接发送接收消息

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | EGW |
| dev_id | String | 是 | 企业开发者ID |
| token | String | 是 | 企业开发者ID对应的[access_token](http://paas.hst.com/developer/document?production=other)  获取接口在1.产品文档2.其他3.准备工作 |
| id | int | 是 | 20000 协议id |


示例：
```js
{
	"business":"EGW",
	"dev_id":"23be7500fa7d6850d976ca473c296db2",
	"token":"60b52680c356c5c29c8393132eaadf92",
	"id":20000
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| id | int | 登录的返回固定为20001 |
| result | int | 返回为0时代表成功，其他返回参考错误码列表 |
| message | String | 提示的消息 |

示例：
```js
{
	"id": 20001,
	"message": "login successful",
	"result": 0
}
```
## 登出事件网关
> 登录之后保持长连接发送接收消息

接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | EGW |
| dev_id | String | 是 | 企业开发者ID |
| token | String | 是 | 企业开发者ID对应的access_token  获取接口在1.产品文档2.其他3.准备工作 |
| id | int | 是 | 20002 协议id |


示例：
```js
{
	"business":"EGW",
	"id":20002
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| id | int | 登出的返回固定为20003 |
| result | int | 返回为0时代表成功，其他返回参考错误码列表 |
| message | String | 提示的消息 |

示例：
```js
{
	"id": 20003,
	"message": "logout successful",
	"result": 0
}
```


## 订阅事件

>订阅某个APPID的事件

### 请求参数说明
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定是EGW  |
| id | int | 是 | 20004 协议ID|
| app_list | json object 数组 | 是 | |
| app_id | string| 是 | 应用ID |

示例：
```js
{
"business":"EGW",
"id":20004,
"app_list":[
		{
		"app_id":"15657845fd30b24e9ceb443e6f0a7bf3"
		}
	]
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| id | int | 是 | 20005 协议ID|
| result | int | 返回为0时代表成功，其他返回参考错误码列表 |
| message | String | 提示的消息 |

示例：
```js
{
	"id": 20005,
	"message": "subscribe successful",
	"result": 0
}
```
## 取消订阅事件

>取消订阅事件  或者取消订阅事件某个APPID的事件

### 请求参数说明
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定是EGW  |
| id | int | 是 | 20006 协议ID|
| app_list | json object 数组 | 是 | |
| app_id | string| 是 | 应用ID |

取消订阅指定APPID示例：
```js
{
    "business":"EGW",
    "id":20006,
    "app_list":[
            {
            	"app_id":"15657845fd30b24e9ceb443e6f0a7bf3"
            }
        ]
}
```
取消订阅示例：
```js
{
    "business":"EGW",
    "id":20006
}
```
### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| id | int | 是 | 20007 协议ID|
| result | int | 返回为0时代表成功，其他返回参考错误码列表 |
| message | String | 提示的消息 |

示例：
```js
{
	"id": 20007,
	"message": "unsubscribe successful",
	"result": 0
}
```

## 获取全量数据

>获取appid下所有在线用户、及广播的媒体数据

### 请求参数说明
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定是EGW  |
| id | int | 是 | 20008 协议ID|
| app_list | json数组 | 是 | APPID数组  |
| app_id | string | 是 | 应用ID|
| group_list | json数组 | 是 | group数组  |
示例：
>指定单个app下面单个组
```js
{
"business":"EGW",
"seq":"1",
"app_list":[
		{
		"app_id":"15657845fd30b24e9ceb443e6f0a7bf3",
		"group_list":["123456"]
		}
],
"id":20008
}
```
>appid所有数据
```js
{
"business":"EGW",
"seq":"1",
"app_list":[
		{
		"app_id":"15657845fd30b24e9ceb443e6f0a7bf3",
		}
],
"id":20008
}
```

### 返回说明

接口的返回类型为JSON。返回字段如下：

| 参数名 | 类型 | 参数说明 |
| - | - | - | - |
| result | int | 返回为0时代表成功，其他返回参考错误码列表 |
| id | int | 是 | 20009 协议ID|
| app_id | String | 提示的消息 |
| group_list | json数组 | 组内的用户及媒体数据 |
| group_media_list | json数组 | 组内的媒体数据（单前是会有白板） |
| media_info | json数组 | 用户广播的音视频、屏幕共享 |
| media_id | string | 标识广播媒体的ID |
| media_type | int | 广播媒体的类型 4：白板 2：音频 1：视频 0：屏幕共享|
| user_id | string | 标识用户的ID |
| group_id | string | 组ID |
| version | int | 事件版本号(同一个APPID下递增连续)|
示例：
```js
{
	"app_id": "15657845fd30b24e9ceb443e6f0a7bf3",
	"group_list": [{
		"group_id": "123456",
		"group_media_list": [{
			"media_id": "whiteboard2",
			"media_type": 4
		}],
		"user_list": [{
			"media_info": [{
				"media_id": "0",
				"media_type": 0
			}, {
				"media_id": "appdef_mic_magic",
				"media_type": 1
			}, {
				"media_id": "LocalCam_2",
				"media_type": 2
			}],
			"user_id": "aa"
		}, {
			"media_info": [],
			"user_id": "ff"
		}]
	}],
	"id": 20009,
	"message": "synchronize all data successful",
	"result": 0,
	"version": 3132
}
```

## 事件广播消息

>服务器主动推送的事件消息

### 请求参数说明
接口的请求类型为JSON。请求字段如下：

| 参数名 | 类型 | 是否必填 | 参数说明 |
| - | - | - | - |
| business | String | 是 | 固定是EGW  |
| id | int | 是 | 20102、20103、20100、20101|
| group_id | string | 是 | 发生事件的组ID |
| user_id | string| 是 | 触发事件的用户ID |
| version | int | 是 | 事件版本号 (不连续时建议全量同步次数据 以保障数据的完整性)|
| media_id | string| 是 | 媒体的ID |
| media_type | int | 是 | 媒体类型|

用户加入组示例：
```js
{
	"group_id": "123456",
	"id": 20100,
	"user_id": "aa",
	"version": 2714
}
```
用户退出组示例：
```js
{
	"group_id": "123456",
	"id": 20101,
	"user_id": "aa",
	"version": 2714
}
```
用户广播流示例：
```js
{
	"group_id": "123456",
	"id": 20102,
	"media_id": "LocalCam_2",
	"media_type": 2,
	"user_id": "aa",
	"version": 2715
}
```
用户停止广播流示例：
```js
{
	"group_id": "123456",
	"id": 20102,
	"media_id": "LocalCam_2",
	"media_type": 2,
	"user_id": "aa",
	"version": 2715
}
```

## 协议ID表

| 协议ID | 释义 | 备注 | 其他 |
| - | - | - | - |
| 20001 | 登录事件网关请求 |   |   |
| 20002 | 登录事件网关响应 |   |   |
| 20003 | 登出事件网关请求 |   |   |
| 20004 | 登出事件网关响应|   |   |
| 20005 | 订阅组事件请求 |   |   |
| 20006 | 订阅组事件响应|   |  |
| 20007 | 取消订阅组事件请求|   |   |
| 20008 | 取消订阅组事件响应 |   |   |
| 20009 | 同步全量请求 |   |   |
| 20010 | 同步全量响应 |   |   |
| 20011 | 心跳请求|   |   |
| 20012 | 心跳响应 |   |   |
| 20101 | 通知用户进入组|   |   |
| 20102 | 通知用户推出组 |   |   |
| 20103 | 通知用户开始广播媒体|   |   |
| 20104 | 通知用户停止广播媒体 |   |   |
