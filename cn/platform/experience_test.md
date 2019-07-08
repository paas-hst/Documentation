
您可以通过Demo程序快速体验好视通云通信平台提供的产品的服务。运行Demo程序有两种方式，第一种方式是直接下载/安装然后运行，点击此处下载Demo； 第二种方式是下载源码编译运行，Demo源码托管在GitHub上，点击此处下载Demo源码。相比较而言，前者更加快捷方便，后者拥有更多控制。

下面以Windows端Demo程序为例，讲解Demo程序特性，其他端Demo程序类似。

## 应用配置
Demo不需要做任何配置即可运行，程序内置了默认的App ID和App Secret。如果您想配置自己创建的App，在登录界面点击“应用配置”按钮，在对话框中进行配置。如果测试的是公有云产品，Server Address使用默认的即可，如果是测试私有云产品，Server Address需要填真实服务器地址，具体格式请参考相关文档或咨询技术支持。

<img alt="demo_app_setting.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_app_setting.png" align="center" />

## 登录界面
登录平台需要输入User ID，User ID用来唯一标识一个用户，需要保证在App下唯一，User ID由开发者定义，只能包含字母、数字和下划线。

<img alt="demo_login.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_login.png" align="center" />

## 在线界面
登录平台后，进入在线界面，此界面能够看到App下所有在线用户。在此界面输入Group ID，Group ID用来唯一标识一个分组，可以认为等同于会议中的房间， 如果希望多人在一个房间中进行交互，则要确保大家填入相同的Group ID，加入相同的分组。一种入会方式是点击“加入分组”按钮，则直接进入主界面；另一种入会方式是邀请入会，从在线用户列表中选择被邀请人，然后点击“邀请并加入分组”，也会进入主界面，但同时会向被选择的在线用户发起邀请入会呼叫，被邀请端会弹出邀请框，用户选择是同意邀请还是拒绝邀请。

<img alt="demo_online.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_online.png" align="center" />
<img alt="demo_invite.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_invite.png" align="center" />

## 主界面
登录成功后会进入Demo主界面。主界面集中展示了好视通云通信平台所提供的服务能力，但不是全部，具体请参考相关文档。

<img alt="demo_main.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_main.png" align="center" />

## 参数设置
点击工具栏的设置按钮，可以对某些功能进行参数设置。

<img alt="demo_setting.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/demo_setting.png" align="center" />
