# 基本概念

## 账号认证
要想使用好视通云通信平台的服务，必须在官网注册账号。只要注册账号，平台就会赠送测试费用。刚注册的账号属于未认证账号，要想获得更高额度的赠送费用，可以根据情况选择认证为“个人开发者”或“企业开发者”。认证为个人开发者，需要提供身份信息；认证为企业开发者，需要提供营业执照信息。 此外，个人开发者可以申请升级为企业开发者。

<img alt="auth.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/auth.png" align="center" />

## App ID和App Secret
应用（App）是客户使用平台产品的桥梁和载体，在使用平台产品之前，必须先创建应用，系统会为每个应用分配App ID和创建App Secret。App ID用来标识一个应用，全平台唯一。App Secret作为加密秘钥，用来生成登录所需的Token，因此，App Secret对于客户的账号安全非常重要，请务必妥善保管。

<img alt="appid.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/appid.png" align="center" />

## Group ID和User ID
Group ID（分组ID）是一个非常重要的概念，平台当前提供的很多服务是基于分组的服务，在使用这些服务之前，需要先加入分组，只有加入到同一个分组的用户才能够进行通信。分组ID由开发者定义，开发者保证在App范围内唯一即可，不同App的Group ID重复不会相互影响。

User ID（用户ID）也非常重要，在登录平台时，必须携带此字段，开发者必须保证App下User ID是唯一的，否则由于会产生User ID冲突而导致登录失败。此字段提供给开发者用来关联业务数据，比如，如果想知道应用中某个用户的计费情况，则可以将Use ID传入，平台会将User ID与所使用的服务关联起来，在导出的计费记录中会带上Use ID。

<img alt="group_user.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/group_user.png" align="center" />

## Video ID
Video ID用来标识一个虚拟的视频源，Video ID由开发者定义，但需要保证同一个User ID下同一时刻Video ID的唯一性。同一用户可以广播多路视频，不同视频通过Video ID区分。

<img alt="video_id.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/video_id.png" align="center" />

假设开发者设置Video ID为“my camera”，并绑定Camera 1，此时远端看到的是Camera 1的视频；如果开发者将“my camera”重新绑定为Camera 2，即切换摄像头，则远端能够立即看到Camera 2的视频。整个切换过程，客户端到服务器以及服务器之间的连接不会重建，用户基本无感知。 

## 应用鉴权
鉴权是判断访问者是否具有合法身份，保障客户账号安全性的必要措施之一。开发者在使用SDK进行登录时，需要携带Token，系统会对Token携带的信息进行校验，如果信息正确则登录成功，否则登录失败。

<img alt="token_desc.png" src="https://raw.githubusercontent.com/paas-hst/Documentation/master/cn/images/platform/token_desc.png" align="center" />

Token在开发者这一侧通过代码生成，[点此](http://paas.hst.com/developer/code)选择对应语言的Token生成代码，开发者需要将此代码集成到自己的服务器中，控制Token的生成和分发。由于Token会使用App Secret进行加密，开发者需要确保App Secret的安全性。考虑到App Secret泄漏的风险，如无特殊情况，不建议将Token生成代码集成到客户端。