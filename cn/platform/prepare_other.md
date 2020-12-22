# 准备工作

好视通云通信平台云录制通过一组API进行控制。
分为录制相关与存储相关两部分接口，要求一定的不同。

## 前提条件

开通云录制功能，请确保账号满足以下身份条件:

-   已申请成为企业开发者并通过审核
-   录制相关接口是http
-   云录制里存储相关接口需要以POST方式请求，formdata格式的数据

## 接口说明

1.  存储相关接口为POST请求。
2.  所有接口返回格式为json，编码方式为utf-8。


## 组成员通知
加入分组后，系统会通过 IFspEngineEventHandler::OnGroupUsersRefreshed 推送当前组内所有成员列表。后续，组内有成员进入或离开，会通过 IFspEngineEventHandler::OnRemoteUserEvent 回调通知上层，开发者可以藉此维护分组内的用户列表。