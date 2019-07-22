# 产品介绍

支持发送自定义消息，用以实现消息通知和基于消息的业务控制，基于TCP传输。

> 发送频率不能超过100次每秒。

## 产品特点

+ 端到端50ms超低延时，可应用于各种实时场景。
+ 支持单播、组播和广播，更加灵活可控。
+ 99.999%的可靠性。


## 应用场景

+ 直播：可用信令通道实现，弹幕、聊天室、权限控制（踢人、禁言、禁麦）等。
+ 社交：可用信令通道实现私聊消息，群消息等实时聊天应用。
+ 教育：可用信令通道实现班级群消息，私聊消息，权限控制（点名、奖励、举手）等。
+ 物联网：可用信令通道实现任何的控制消息发送。

## 产品规格

<table>
<tr>
<th colspan="2" align="center">规格项</th>
<th align="center">规格说明</th>
</tr>

<tr>
<td rowspan="4">功能规格</td>
<td>点对点消息</td>
<td >指定单一接收方发送消息</td>
</tr>

<tr>
<td>广播消息</td>
<td>分组内广播消息到所有终端</td>
</tr>

<tr>
<td>黑名单</td>
<td>除指定名单外，向分组内其他所有终端发送消息</td>
</tr>

<tr>
<td>白名单</td>
<td>只发送消息到分组内指定终端</td>
</tr>


<tr>
<td rowspan="3">参数规格</td>
<td>消息最大长度</td>
<td>8KB</td>
</tr>

<tr>
<td>白名单最大数量</td>
<td>128</td>
</tr>

<tr>
<td>黑名单最大数量</td>
<td>128</td>
</tr>

</table>


## 平台兼容性

<table>
<tr>
<th colspan="2" align="center">规格/平台</th>
<th align="center">Windows</th>
<th align="center">Android</th>
<th align="center">iOS</th>
<th align="center">macOS</th>
<th align="center">Web</th>
<th align="center">WeChat</th>
</tr>

<tr>
<td rowspan="4">功能规格</td>
<td>点对点消息</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>广播消息</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>黑名单</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>白名单</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
</tr>


<tr>
<td rowspan="3">参数规格</td>
<td>消息最大长度</td>
<td align="center">8KB</td>
<td align="center">8KB</td>
<td align="center">8KB</td>
<td align="center">8KB</td>
<td align="center">8KB</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>白名单最大数量</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>黑名单最大数量</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">128</td>
<td align="center">&#10005</td>
</tr>

</table>

> 对号表示支持，叉号表示不支持，“-”表示不确定。