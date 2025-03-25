# 准备工作

平台大部分服务是基于分组的服务，因此，在使用服务前需要加入分组（Group），在加入分组前，需要先登录平台，具体如下所述。

## 前提条件

请确保满足以下开发环境要求:

- HarmonyOS SDK API Version ≥ 5.0.0(12)

- DevEco Studio 5.0.0 Release 或以上版本

- 设备要求 HarmonyOS 5.0.0 或以上版本

## 添加 SDK

1.  下载 [HarmonyOS NEXT SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2.  将 `.har` 文件拷贝到项目的 `libs` 目录下。
3.  在模块的 `oh-package.json5` 文件中添加依赖：
```JSON
{
    "dependencies": {
        "@third/hstfspsdk": "file:libs/HstFspSdk.har"
    }
}
```
4.  在`module.json5`中添加请求权限：
```JSON
{
    "requestPermissions": [
      {
        "name": "ohos.permission.INTERNET",
        "reason": "$string:reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.STORE_PERSISTENT_DATA",
        "reason": "$string:reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.GET_NETWORK_INFO",
        "reason": "$string:reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.MICROPHONE",
        "reason": "$string:reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.CAMERA",
        "reason": "$string:reason",
        "usedScene": {
          "when": "always"
        }
      }
    ]
}
```

## 初始化

使用SDK之前必须初始化。

```TYPESCRIPT
// 创建引擎实例
let fspEngine = FspEngine.create(context, appId, null, this);

// 初始化引擎
fspEngine.init();
```

> 需要注意，引擎是单例，一个进程只能有一个实例，重复初始化可能会引起未知异常。

## 登录平台

初始化完成后，就可以登录平台了，登录需要使用到Token、User ID、ForceLogin、CusName。其中，Token为字符串，用来校验身份和鉴权，由开发者自己生成，具体请参考“平台介绍->基本概念->应用鉴权”；User ID也是字符串，由开发者定义，用来唯一标识一个用户，开发者必须保证App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```TYPESCRIPT
fspEngine.login(token, userId, forceLogin, cusName);
```

> User ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

可以通过onLoginResult回调获得登录结果。


## 加入分组

平台的很多服务都是基于分组来提供的，登录成功后，需要加入分组。Group ID由开发者自己定义，但必须确保App下唯一，具体请参考“平台介绍->基本概念->Group ID和User ID”。

```java
fspEngine.joinGroup(groupId);
```

> Group ID定义必须符合规则：长度不超过128，只能是字母、数字、下划线(_)和横杠(-)。

可以通过onJoinGroupResult回调获得加入分组结果。

## 分组成员列表
加入分组后，可以通过onGroupUsersRefreshed回调来获取分组成员列表，这个回调只会在加入分组时回调一次，推送全量用户列表。后续分组内成员列表的更新：加入和离开，会通过onRemoteUserEvent回调来通知上层应用，开发者可以基于这两个回调来实时维护分组内用户列表。
