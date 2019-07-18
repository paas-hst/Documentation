# 集成客户端
本文如何集成Mac SDK, 需要准备的开发环境，包含前提条件及SDK集成方法等内容。

## 前提条件
请确保满足以下开发环境要求:

- Xcode 10.0+
- mac OS 10.11+
- 请确保您的项目已设置有效的开发者签名

## 创建项目并获取 App ID

1. [点此注册](http://customer.paas.hst.com/register)，按照步骤注册账号，创建应用。
2. 配置使用相关产品并上线应用。
3. 点击 **应用** 下的**应用列表** ，在详情页面获取到 **App ID**。

## 添加SDK
1. 下载[Mac SDK](http://paas.hst.com/developer/downloadSDK)，解压并打开。

2. 使用 Xcode 打开你想要运行的项目，然后选中当前 Target。
3. Build Phases 页签，展开 Link Binary with Libraries 项并添加如下库。点击 + 图标开始添加
![tokendesc](../images/mac_Integrate.png)
+ VideoToolbox.framework
+ CoreAudio.framework
+ AudioToolbox.framework
+ CoreMedia.framework
+ VideoDecodeAcceleration.framework
+ libiconv.tbd
+ libz.tbd
+ libc++.tbd
