# 集成客户端
本文如何集成Android SDK，需要准备的开发环境，包含前提条件及 SDK 集成方法等内容。

## 前提条件

请确保满足以下开发环境要求:

- Android SDK API Level Level ≥ 17

- Android Studio 3.0 或以上版本

- App 要求 Android 4.1 或以上设备

## 创建项目并获取 App ID

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。
2. 配置使用相关产品并上线应用。
3. 点击 **应用** 下的**应用列表** ，在详情页面获取到 **App ID**。

## 添加 SDK

1.  下载 [Android SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2.  aar库拷贝到 app/libs 目录下
3.  app的gradle脚本中正确引用到aar库，比如：implementation(name: 'fsp_sdk', ext: 'aar')

现在你已经设置好了 Android Studio 开发环境，可以开始使用 Android SDK 了！

> 目前所有产品的接口在一个SDK内提供，集成后，可以开始所有产品的功能开发。

## 相关文档
完成了客户端集成后，你可以使用 SDK，使用各个产品的功能：

- [准备工作](../prepare_android.md)
