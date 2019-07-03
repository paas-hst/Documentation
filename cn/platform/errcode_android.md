# 错误码
SDK大部分方法有错误码，或者回调方法有错误码参数，错误码是定义 在FspEngine 类里ERR_ 开头的常量。

## ErrCode 定义

```java
class FspEngine{
    /** 成功 */
    public static final int ERR_OK = 0;

    /** 非法参数 */
    public static final int ERR_INVALID_ARG = 1;
    /** 非法状态 */
    public static final int ERR_INVALID_STATE = 2;
    /** 内存不足 */
    public static final int ERR_OUTOF_MEMORY = 3;
    /** 访问设备失败 */
    public static final int ERR_DEVICE_FAIL = 4;
    /** 网络连接失败 */
    public static final int ERR_CONNECT_FAIL = 30;
    /** 没加入组 */
    public static final int ERR_NO_GROUP = 31;
    /** 认证失败 */
    public static final int ERR_TOKEN_INVALID = 32;
    /** app不存在，或者app被删除 */
    public static final int ERR_APP_NOT_EXIST = 33;
    /** 相同userId已经加入同一个组，无法再加入 */
    public static final int ERR_userId_CONFLICT = 34;
    /** 没有登录 */
    public static final int ERR_NOT_LOGIN = 35;
    /** 账户余额不足 */
    public static final int ERR_NO_BALANCE = 70;
    /** 没有视频权限 */
    public static final int ERR_NO_VIDEO_PRIVILEGE = 71;
    /** 没有音频权限 */
    public static final int ERR_NO_AUDIO_PRIVILEGE = 72;
    /** 服务内部错误 */
    public static final int ERR_SERVER_ERROR = 301;
    /** 操作失败 */
	public static final int ERR_FAIL = 302;
}
```