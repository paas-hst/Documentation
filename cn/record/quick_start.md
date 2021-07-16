# 快速开始

## 获取Access Token
>使用[接口](http://paas.hst.com/developer/document?production=other)获取开发者ID对应的访问token
调用录制的所有接口都有使用到 [access_token](http://paas.hst.com/developer/document?production=other)
使用方式
HTTP header. 在HTTP请求头Authorization中填[access_token](http://paas.hst.com/developer/document?production=other)值



## 请求地址
公有云：https://access.paas.hst.com/server/address?appType=10&app_id=xxxxxxxx 获取
私有云：http://your-server-ip:28000/




## 简化步骤

### 手动录制
>1.初始化录制任务 
2.设置合成效果
3.查询任务列表
4.结束录制任务
5.查询任务列表
6.下载录制文件
**没有用户事件来源时--》可以登录时间网关订APPID阅事件获取事件参数用于动态实时设置布局信息**


### 自动录制
>1.初始化录制任务
2.查询任务列表
3.结束任务任务
4.查询任务列表
5.下载录制文件


## 说明
>查询任务列表 对应的**任务状态(status)是6**且**文件大小(file_size)不为 0** 这个两个条件满足才可以调用下载接口否则返回失败。

| status值 | 状态 | 其他 |
| - | - | - | - |
| -1 | 错误 |   |
| 0 | 成功 |  |
| 1 | 初始化 |   |
| 2 | 录制中 |   |
| 3 | 排队等待编码 |    |
| 4 | 编码中 |   |
| 5 | 上传中 |   |
| 6 | 完成 |  |
| 7 | 暂停 |  |
