# 集成客户端
本文将介绍如何集成Windows SDK，需要准备的开发环境，包含前提条件及 SDK 集成方法等内容。

## 前提条件

请确保满足以下开发环境要求:

-   操作系统： Microsoft Windows 7+

-   编译器：Microsoft Visual C++ 2015+

-   开发环境：Microsoft Visual Studio 2015 （推荐）

## 创建项目并获取 App ID

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。
2. 配置使用相关产品并上线应用。
3. 点击 **应用** 下的**应用列表** ，在详情页面获取到 **App ID**。

## 添加 SDK

1.  下载 [Windows SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。
2.  将 `sdk/include` 目录添加到项目的 INCLUDE 目录下。
3.  将 `sdk/lib` 目录放入项目的 LIB 目录下，并确认 fsp_sdk.lib 与项目有链接。 
4.  将 `sdk/bin` 下的 bin 文件复制到你的可执行文件所在的目录下。

现在你已经设置好了 Windows 开发环境，可以开始使用 Windows SDK 了！

> 目前所有产品的接口在一个SDK内提供，集成后，可以开始所有产品的功能开发。

## 相关文档
完成了客户端集成后，你可以使用 SDK，使用各个产品的功能：

- [准备工作](../prepare_windows.md)
