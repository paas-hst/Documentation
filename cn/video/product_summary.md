# 产品介绍
视频通信可实现一对一或多方同时进行视频互动。视频通信产品本身不包含音频能力，如果需要实现视频通话功能，需要组合使用音频通信产品。

## 产品特点

+ 支持1080P超清视频。
+ 支持本地多摄像头。
+ 支持摄像头热插拔识别。
+ 支持单分组10000并发。
+ 支持RTSP插件。
+ 能抵抗最高40%的丢包不卡顿。

## 应用场景

+ 视频通话：可实现类似微信一样的一对一或多人视频通话。
+ 视频会议：多方视频互动进行会议讨论和分享。

## 产品规格


<table>
<tr>
<th colspan="2" align="center">规格项</th>
<th align="center">规格说明</th>
</tr>

<tr>
<td rowspan="6">功能规格</td>
<td>RTSP插件</td>
<td >通过RTSP插件接入第三方视频源</td>
</tr>

<tr>
<td>热插拔</td>
<td>支持摄像头设备热插拔识别</td>
</tr>

<tr>
<td>视频降噪</td>
<td>去除采集上来视频的噪点</td>
</tr>

<tr>
<td>硬件加速</td>
<td>使用GPU等硬件来进行视频编解码、合成的加速</td>
</tr>

<tr>
<td>H.264</td>
<td>应用最广的高性能视频编码器</td>
</tr>

<tr>
<td>H.265</td>
<td>更高压缩比、更节省带宽的视频编码器</td>
</tr>

<tr>
<td rowspan="6">参数规格</td>
<td>最大采集分辨率</td>
<td>1080P</td>
</tr>

<tr>
<td>最大传输分辨率</td>
<td>1080P</td>
</tr>

<tr>
<td>最大码率</td>
<td>3Mbps</td>
</tr>

<tr>
<td>最大帧率</td>
<td>30fps</td>
</tr>

<tr>
<td>本地最大支持摄像头数量</td>
<td>6</td>
</tr>

<tr>
<td>最大抵抗丢包率</td>
<td>40%</td>
</tr>

</table>

> 最大码率只是一个大概值，当前SDK不支持手动设置码率，SDK内部会根据当前分辨率和网络状况自动调节码率。

## 平台兼容性

<table>
<tr>
<th colspan="2" align="center">规格/平台</th>
<th>Windows</th>
<th>Android</th>
<th>iOS</th>
<th>macOS</th>
<th>Web</th>
<th>WeChat</th>
<th>Harmony</th>
</tr>

<tr>
<td rowspan="6">功能规格</td>
<td>RTSP插件</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>热插拔</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#8211</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
</tr>

<tr>
<td>视频降噪</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
</tr>

<tr>
<td>硬件加速</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#8211</td>
<td align="center">&#8211</td>
<td align="center">&#10003</td>
</tr>

<tr>
<td>H.264编码</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
</tr>

<tr>
<td>H.265编码</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10003</td>
<td align="center">&#10005</td>
<td align="center">&#10005</td>
<td align="center">&#10003</td>
</tr>

<tr>
<td rowspan="6">参数规格</td>
<td>最大采集分辨率</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">&#8211</td>
<td align="center">1080P</td>
</tr>

<tr>
<td>最大传输分辨率</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">1080P</td>
<td align="center">&#8211</td>
<td align="center">1080P</td>
</tr>

<tr>
<td>最大码率</td>
<td align="center">3Mbps</td>
<td align="center">3Mbps</td>
<td align="center">3Mbps</td>
<td align="center">3Mbps</td>
<td align="center">&#8211</td>
<td align="center">&#8211</td>
<td align="center">3Mbps</td>
</tr>

<tr>
<td>最大帧率</td>
<td align="center">30fps</td>
<td align="center">30fps</td>
<td align="center">30fps</td>
<td align="center">30fps</td>
<td align="center">&#8211</td>
<td align="center">&#8211</td>
<td align="center">30fps</td>
</tr>

<tr>
<td>本地最大支持摄像头数量</td>
<td align="center">6</td>
<td align="center">2</td>
<td align="center">2</td>
<td align="center">6</td>
<td align="center">&#8211</td>
<td align="center">2</td>
<td align="center">2</td>
</tr>

<tr>
<td>最大抵抗丢包率</td>
<td align="center">40%</td>
<td align="center">40%</td>
<td align="center">40%</td>
<td align="center">40%</td>
<td align="center">&#8211</td>
<td align="center">&#8211</td>
<td align="center">40%</td>
</tr>

</table>

> 对号表示支持，叉号表示不支持，“-”表示不确定。
