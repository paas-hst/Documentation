# 准备工作

在调用业务网关接口时，需要携带Access Token，服务器会对Access Token进行鉴权。

## 什么是Access Token

Access Token是长度为32的随机字符串。它的有效时长是7200秒（也就是两小时），超过7200秒会失效，失效后接口返回的状态码code为606000001，此时需要重新获取一个Access Token。

对于一个PaaS公有云账户来说，同一时刻只会有一个生效的Access Token，每次获取新的Access Token都会覆盖旧的。所以在你的系统中，Access Token最好全局托管，比如提供一个专门管理Access Token的服务（或者一个模块），所有对Access Token的访问都调用此服务的方法。

> 获取Access Token的方法需要设置成线程安全的，因为多个线程并发调用可能会导致互相覆盖返回结果。

## 如何获取Access Token

### 请求方式
HTTP或HTTPS协议，GET方法

### 请求地址
公有云：https://fsp-store-gw.hst.com/access/token
私有云：http://your-server-ip:28000/access/token

### 请求参数
| 参数名 | 类型 | 是否必需 | 参数说明 |
| :-: | :-: | :-: | - |
| dev_id | String | 是 | 开发者ID |
| token | String | 是 | 使用开发者ID和开发者秘钥生成的token |

利用好视通PaaS官网提供的[FspToken](https://github.com/paas-hst/TokenGenerator_java)来生成token。开发者ID对应FspToken工具类中的App ID，开发者秘钥对应secretkey,其他参数可以不填。

> 开发者ID和秘钥通过PaaS管理平台的面板页面获取。

### 传参方式
HTTP header. 在HTTP请求头Authorization中携带开发者ID和Token，两者用”.”隔开，例如：459d0e780b96ce2c42b6356a67e5e35c.k5FUR5LlEoTq5t1ZZ1A9RoQfqgbL1mtJ4DzMdwOW7tvaZZqhXtm6rsisnyoYo9S0HPTDBZGMMhii4gLAorBdCSxb0Iv0yBfFehUTW76gAUm7QuSo3ZqTMvsV
前面那一段是开发者ID，后面那一段是token.

### 响应结果
| 参数名 | 类型 | 参数说明 |
| :-: | :-: | - |
| access_token | String | 接口凭证 |
| timeout | int | access_token有效时长，单位:秒 |

示例：
```js
//成功结果示例
{
	"code": 0,
	"msg": "OK",
	"result": {
		"timeout": 7200,
		"access_token": "f0f646c66a7219b040e45fdb592504ba"
	}
 }

//失败结果示例
{
	"code": 606000000,
	"msg": "Authentication failed"
}
```

### 接口地址（业务网关）
公有云: https://fsp-store-gw.hst.com
私有云: http://your-server-ip:28000

### 响应结果
| 名称 | 类型 | 参数说明 |
| :-: | :-: | - |
| code | int | 返回为0时代表成功，其他返回参考错误码列表 |
| msg | String | 提示信息 |

### 响应格式
application/json;charset=UTF-8