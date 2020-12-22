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
