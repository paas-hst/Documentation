# 错误码
SDK大部分方法有错误码，或者回调方法有错误码参数，错误码是定义为 ErrCode 枚举。

## ErrCode 定义

```
/**
 * 错误码集合
 */
enum ErrCode {
	ERR_OK = 0, ///<成功

	ERR_INVALID_ARG = 1,      ///<非法参数
	ERR_INVALID_STATE = 2,    ///<非法状态
	ERR_OUTOF_MEMORY = 3,     ///<内存不足
	ERR_DEVICE_FAIL = 4,      ///<访问设备失败

	ERR_CONNECT_FAIL = 30,     ///<网络连接失败
	ERR_NO_GROUP = 31,         ///<没加入组
	ERR_TOKEN_INVALID = 32,    ///<认证失败
	ERR_APP_NOT_EXIST = 33,    ///<app不存在，或者app被删除
	ERR_USERID_CONFLICT = 34,  ///<相同userid已经加入同一个组，无法再加入

	ERR_NO_BALANCE = 70,         ///<账户余额不足
	ERR_NO_VIDEO_PRIVILEGE = 71, ///<没有视频权限
	ERR_NO_AUDIO_PRIVILEGE = 72, ///<没有音频权限

	ERR_NO_SCREEN_SHARE = 73,    ///<当前没有屏幕共享

	ERR_RECVING_SCREEN_SHARE = 74,   ///<当前正在接收屏幕共享

	ERR_SERVER_ERROR = 301,	    ///服务内部错误
	ERR_FAIL = 302              ///<操作失败
};
```